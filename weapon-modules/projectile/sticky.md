---
description: Create sticky bombs and let projectiles stick to walls/entities
---

# Sticky

```yaml
    Sticky:
      Blocks:
        Allow_Any: <true/false>
        Whitelist: <true/false>
        List:
          - <Material>
          - <etc.>
      Entities:
        Allow_Any: <true/false>
        Whitelist: <true/false>
        List:
          - <EntityType>
          - <etc.>
```

#### Blocks

* `Allow_Any`
  * If this is true then the projectile can stick to all blocks.
  * This overrides `Whitelist` and `List`.
* `Whitelist`
  * Whether the use `List` as whitelist or blacklist.
  * `True` = only blocks listed in `List` can be stuck to.
* `List`
  * Material list of stickable/unstickable blocks depending on `Whitelist`.
  * Use the [Material](https://app.gitbook.com/s/IIUkVnlH40vVBzLhWWQ8/references#material "mention") list for materials for your version.

#### Entities

* `Allow_Any`
  * If this is true then all entities are stickable.
  * This overrides `Whitelist` and `List`.
* `Whitelist`
  * Whether the use `List` as whitelist or blacklist.
  * `True` = only entities listed in `List` can be sticked to.
* `List`
  * Entity list of stickable/unstickable entities depending on `Whitelist`.
  * Use the [entity](https://app.gitbook.com/s/IIUkVnlH40vVBzLhWWQ8/references#entity "mention") list for entities for your version.
