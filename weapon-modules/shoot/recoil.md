# Recoil

Recoil moves the player's screen horizontally and/or vertically. This simulates rifle recoil, and makes the gun harder to control.

More technically, every shot

```yaml
    Recoil:
      Mean_X: <number>
      Mean_Y: <number>
      Variance_X: <number>
      Variance_Y: <number>
      Speed: <number>
      Damping: <number>
      Damping_Recovery: <number>
      Smoothing: <number>
      Max_Accumulation: <number>
```

#### Mean\_X/Y

A base, guaranteed recoil offset on each shot. For example, `Mean_Y: 1.5` means each shot tends to push the view up by
around 1.5 degrees. This is your "main recoil" config, and you tweak these values to increase/decrease the recoil.

This value is measured in degrees.

#### Variance\_X/Y

Adds random variation around the mean value. For example, if `Mean_X: 0.2` and `Variance_X: 0.3`, each shot can be anywhere
from `-0.1` to `+0.5` horizontally. Larger variances = less predictable spread. 

This value is measured in degrees.

#### Speed

How snappy or forceful the recoil "kick" is each tick. Higher values = stronger immediate kick.

Each tick, the difference between the current offset and the target offset is multiplied by this speed
value. Typically, you might use a value in the range `[2, 6]`. An automatic weapon, or weapon with less
recoil should probably have a value closer to 2. A larger caliber weapon, like a sniper rifle, should have 
a value closer to 6.

#### Damping

Each tick, the "target recoil" is multiplied by `(1 - damping)`. This prevents infinite buildup
when shooting rapidly. For example, `Damping: 0.1` means each tick, the stored "target" recoil
shrinks by 10%. 

#### Damping_Recovery

How quickly your *current* recoil recovers to 0. Larger values pull the camera back down faster 
after each shot.

#### Smoothing
A factory (0.0 to 1.0) that controls how "smoothly" the camera transitions to its new recoil offset.
Lower values = more abrupt. Higher values = more fluid. 

#### Max_Accumulation
Maximum total recoil allowed before we clamp it off. Useful to stop a fully automatic weapon from
pushing the camera infinitely high. 

In general, you should prefer to use [#damping](recoil.md#damping "mention") to limit the recoil.
