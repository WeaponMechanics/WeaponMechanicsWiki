---
description: Let projectiles bounce and reflect off of blocks and entities
---

# Bouncy

```yaml
    Bouncy:
      Maximum_Bounce_Amount: <amount>
      Blocks:
        Allow_Any: <true/false>
        Default_Speed_Multiplier: <multiplier>
        Whitelist: <true/false>
        List:
          - <Material>
          - <Material> <speed multiplier>
          - <etc.>
      Entities:
        Allow_Any: <true/false>
        Default_Speed_Multiplier: <multiplier>
        Whitelist: <true/false>
        List:
          - <EntityType>
          - <EntityType> <speed multiplier>
          - <etc.>
      Rolling:
        Required_Motion_To_Start_Rolling: <speed>
        Blocks:
          Allow_Any: <true/false>
          Default_Speed_Multiplier: <multiplier>
          Whitelist: <true/false>
          List:
            - <Material>
            - <Material> <speed multiplier>
            - <etc.>
```

#### Maximum\_Bounce\_Amount

The maximum amount this projectile can bounce off from entities and blocks.\
Defaults to `1`. Setting value to `-1` means infinite.

**`Blocks`:**

* `Allow_Any`
  * If this is true then all blocks are valid.
  * This overrides `Whitelist` and `List`.
* `Default_Speed_Multiplier`
  * The number to multiply the projectile speed by.
  * This is the default speed multiplier, meaning that if the following list does not contain specific information for speed about the hit block, then it defaults to this value.
* `Whitelist`
  * Whether the use `List` as whitelist or blacklist.
  * `True` = only blocks listed in `List` can be bounced off.
* `List`
  * Material list of bounceable blocks depending on `Whitelist`.
  * Use the [Material](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/references#material "mention") list for your version.
  * The second argument is `speed multiplier` which multiplies the projectile's current speed with its value.

#### Entities

* `Allow_Any`
  * If this is true then all entities are valid.
  * This overrides `Whitelist` and `List`.
* `Default_Speed_Multiplier`
  * The number to multiply the projectile speed by.
  * This is the default speed multiplier, meaning that if the following list does not contain specific information for speed about the hit entity, then it defaults to this value.
* `Whitelist`
  * Whether the use `List` as whitelist or blacklist.
  * `True` = only entities listed in `List` can be bounced off.
* `List`
  * Entity list of bounceable entities depending on `Whitelist`.
  * Use the [entity](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/references#entity "mention") list for your version.
  * Second argument is `speed multiplier` which multiplies the projectile's current speed with its value.

#### Rolling

This is useful for grenades for example. First, you want them to bounce off walls and when the motion gets low enough they'll just start rolling on the ground. When the motion of the projectile decreases to near `0`, it is automatically stuck to the current block below.

* `Required_Motion_To_Start_Rolling`
  * Defines the required motion to start rolling.
  * When the speed of projectile goes below this value, it will start rolling instead of bouncing
* `Blocks`
  * Same as above `Blocks` configuration, but used with rolling and the speed multiplier is based on the block below the projectile.
