---
description: Add a bayonet to your gun, or create melee weapons like baseball bats
---

# Melee

```yaml
  Melee:
    Enable_Melee: <true/false>
    Melee_Attachment: <melee weapon name>
    Melee_Range: <maximum melee range>
    Melee_Hit_Delay: <ticks>
    Melee_Miss:
      Mechanics: <Mechanics>
      Melee_Miss_Delay: <ticks>
      Consume_On_Miss: <true/false>
```

#### Enable\_Melee

Use `true` if this weapon is a melee weapon, like a knife, a bat, or a lightsaber. Otherwise, use the `Melee_Attachment` option (for bayonets).&#x20;

#### Melee\_Attachment

Gives this weapon a non-removable bayonet. For example, if you have a melee weapon called `Tactical_Knife`, then use:

```yaml
  Melee:
    Melee_Attachment: Tactical_Knife
```

Your weapon will now "_inherit_" the melee properties of the knife.

#### Melee\_Range

How far the melee can hit people from. For best results, I recommend deleting this option altogether, which instead uses Minecraft's built in melee system.

#### Melee\_Hit\_Delay

The time in ticks (20 ticks = 1 second) between hits that deal damage.&#x20;

#### Melee\_Miss

* `Mechanics`
  * Mechanics triggered when you miss.
  * Use [Mechanics](http://127.0.0.1:5000/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") wiki.
  * To trigger mechanics on HITS, use [#mechanics](damage/#mechanics "mention") from damage.&#x20;
* `Melee_Miss_Delay`
  * The time in ticks before you can hit again.
* `Consume_On_Miss`
  * When set to `true`, consumes ammo (if configured), durability (if configured), etc.
