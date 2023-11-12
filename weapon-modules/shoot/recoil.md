# Recoil

Recoil moves the player's screen horizontally and/or vertically. This simulates rifle recoil, and makes the gun harder to control.

```yaml
    Recoil:
      Push_Time: <push time in millis>
      Recover_Time: <recover time in millis>
      Horizontal:
        - <horizontal recoil>
        - <etc.>
      Vertical:
        - <vertical recoil>
        - <etc.>
      Recoil_Pattern:
        Repeat_Pattern: <true/false>
        List:
          - <horizontal recoil>-<vertical recoil>-<chance to skip>%
          - <etc.>
      Modify_Recoil_When:
        Zooming: <amount> or <amount>%
        Sneaking: <amount> or <amount>%
        Standing: <amount> or <amount>%
        Walking: <amount> or <amount>%
        Riding: <amount> or <amount>%
        Sprinting: <amount> or <amount>%
        Dual_Wielding: <amount> or <amount>%
        Swimming: <amount> or <amount>%
        In_Midair: <amount> or <amount>%
        Gliding: <amount> or <amount>%
```

#### Push\_Time

The time, in milliseconds, it takes to reach the full recoil amount. Higher numbers = worse performance, but smoother movement.

Use `0` to instantly push to the full recoil amount (suggested for automatic rifles).

#### Recover\_Time

The time, in milliseconds, it takes to recover back to the player's starting yaw/pitch.&#x20;

{% hint style="info" %}
After `Push_Time` is complete, there is a 60-millisecond cooldown before recovery starts.
{% endhint %}

#### Horizontal

The list of horizontal recoil amounts. WeaponMechanics randomly chooses 1 value from the list for each shot.&#x20;

{% hint style="info" %}
left=negative numbers, right=positive numbers. Values `<10` are recommended.&#x20;
{% endhint %}

#### Vertical

The list of vertical recoil amounts. WeaponMechanics randomly chooses 1 value from the list for each shot.

{% hint style="info" %}
down=negative numbers, up=positive numbers. Values `<10` are recommended.
{% endhint %}

#### Recoil\_Pattern

This pattern lets you define an ordered list to form a precise pattern. Unlike [#horizontal](recoil.md#horizontal "mention") and [#vertical](recoil.md#vertical "mention") (Which are chosen randomly), this option lets you define the exact order.&#x20;

This option overrides [#horizontal](recoil.md#horizontal "mention") and [#vertical](recoil.md#vertical "mention").

* `Repeat_Pattern`
  * `true` -> After reaching the end of the pattern, loop back to the beginning.&#x20;
  * `false` -> After reaching the end of the pattern, use [#horizontal](recoil.md#horizontal "mention") and [#vertical](recoil.md#vertical "mention") instead.&#x20;
* `List`
  * Format is `<horizontal> <vertical> <skipChance>`
  * `<skipChance>` should be a number between 0 and 100. Defaults to 0.&#x20;

#### Modify\_Recoil\_When

Same as [#modify\_spread\_when](spread.md#modify\_spread\_when "mention"), but for recoil.
