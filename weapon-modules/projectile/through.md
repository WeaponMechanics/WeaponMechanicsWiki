---
description: Projectiles pierce through walls to "wall bang" kill entities
---

# Through

```yaml
    Through:
      Maximum_Through_Amount: <amount>
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
```

#### Maximum\_Through\_Amount

The maximum amount of this projectile can go through entities and blocks.\
Defaults to `1`. Setting value to `-1` means infinite.

#### Blocks

* `Allow_Any`
  * If this is true then all blocks are valid.
  * This overrides `Whitelist` and `List`.
* `Default_Speed_Multiplier`
  * The number to multiply the projectile speed by.
  * This is the default speed multiplier, meaning that if the following list does not contain specific information for speed about the hit block, then it defaults to this value.
* `Whitelist`
  * Whether the use `List` as whitelist or blacklist.
  * `True` = only blocks listed in `List` can be passed through.
* `List`
  * Material list of valid blocks depending on `Whitelist`.
  * Use the [Material](https://app.gitbook.com/s/IIUkVnlH40vVBzLhWWQ8/references#material "mention") list for your version.
  * Second argument is `speed multiplier` which multiplies the projectile's current speed with its value.

#### Entities

* `Allow_Any`:&#x20;
  * If this is true then all entities are valid.
  * This overrides `Whitelist` and `List`.
* `Default_Speed_Multiplier`
  * The number to multiply the projectile speed by.
  * This is the default speed multiplier, meaning that if the following list. does not contain specific information for speed about the hit entity, then it defaults to this value.
* `Whitelist`
  * Whether the use `List` as whitelist or blacklist.
  * `True` = only entities listed in `List` can be passed through.
* `List`
  * Entity list of valid entities depending on `Whitelist`.
  * Use the [entity](https://app.gitbook.com/s/IIUkVnlH40vVBzLhWWQ8/references#entity "mention") list for your version.
  * The second argument is `speed multiplier` which multiplies the projectile's current speed with its value.
