---
description: Configure weapon durability, depletion behavior, and repair kits
---

# Durability and Repair

WeaponMechanics uses Minecraft's normal item damage system. A weapon may lose durability when it shoots or breaks blocks, then either break or remain disabled until repaired.

## Weapon durability

Define the maximum durability inside `Info.Weapon_Item`:

```yaml
  Info:
    Weapon_Item:
      Type: "IRON_HOE"
      Durability:
        Max_Damage: 1000
        Damage: 0
```

* `Max_Damage` -> Maximum item damage.
* `Damage` -> Starting damage. `0` is fully repaired, while `Max_Damage` is depleted.

The `<durability>` and `<max_durability>` placeholders may be used in supported weapon displays.

## Durability per shot

```yaml
  Shoot:
    Durability_Per_Shot: 10
```

`Durability_Per_Shot` is applied after each successful shot. It defaults to `1`. Use `0` to disable durability loss from shooting.

Single, burst, and fully automatic weapons stop firing as soon as the weapon becomes depleted.

## Depletion behavior

```yaml
  Info:
    Durability:
      On_Depleted: DISABLE

    Weapon_Break_Mechanics:
      - "Sound{sound=entity.item.break}"
      - "Message{message=<red>Your weapon broke!}"

    Weapon_Depleted_Mechanics:
      - "Sound{sound=entity.item.break}"
      - "Message{message=<red>Your weapon requires repairs.}"
```

`On_Depleted` supports:

* `BREAK` -> Removes the weapon when it reaches maximum damage. This is the default.
* `DISABLE` -> Keeps the weapon at maximum damage and prevents it from being used until repaired.

`Weapon_Break_Mechanics` is used for `BREAK`. `Weapon_Depleted_Mechanics` is used for `DISABLE`. The selected mechanics run once when the weapon first becomes depleted.

## Repair kits

Repair kits are defined globally in `plugins/WeaponMechanics/config.yml`:

```yaml
Repair:
  Enabled: true

  Kits:
    Basic_Repair_Kit:
      Item:
        Type: "IRON_NUGGET"
        Name: "<yellow>Basic Weapon Repair Kit"
        Lore:
          - "<gray>Repairs <white>25 <gray>weapon durability."
        Custom_Model_Data: 1
      Repair_Amount: 25
      Consume_Item: true

    Advanced_Repair_Kit:
      Item:
        Type: "GOLD_NUGGET"
        Name: "<gold>Advanced Weapon Repair Kit"
        Lore:
          - "<gray>Repairs <white>75 <gray>weapon durability."
        Custom_Model_Data: 1
      Repair_Amount: 75
      Consume_Item: true

  Allow_Repair_While_Full: false
  Allow_Repair_While_Reloading: false
  Allow_Repair_While_Shooting: false
  Excess_Repair_Is_Wasted: true
```

* `Repair_Amount` -> Damage removed from the weapon. Must be at least `1`.
* `Consume_Item` -> Whether one kit is consumed after a successful repair.
* `Allow_Repair_While_Full` -> Whether a kit may be used on a fully repaired weapon.
* `Allow_Repair_While_Reloading` -> Whether an equipped weapon may be repaired while reloading.
* `Allow_Repair_While_Shooting` -> Whether an equipped burst or fully automatic weapon may be repaired while shooting.
* `Excess_Repair_Is_Wasted`
  * `true` -> Repairs up to full and consumes the kit even when part of its repair amount is unnecessary.
  * `false` -> Rejects the repair when the kit would repair more damage than the weapon is missing.

Each weapon must list the kits it accepts:

```yaml
  Repair:
    Allowed_Kits:
      - Basic_Repair_Kit
      - Advanced_Repair_Kit
```

Kit names must exactly match a kit under `Repair.Kits`. Unknown names produce a configuration error.

### Giving and using kits

Give a configured kit with:

```text
/wm repairkit <target> <kit> [amount]
```

Permission:

```text
weaponmechanics.commands.repairkit
```

To repair a weapon:

1. Pick up the repair kit with the inventory cursor.
2. Left-click or right-click the kit onto an allowed damaged weapon in the player's inventory.

The generated kit contains an internal WeaponMechanics tag. Renaming a normal item to match the kit does not make it valid.

## Mending

Mending works because weapon durability uses Minecraft's normal item damage value. Collecting experience while the weapon is in a Mending-compatible slot repairs it normally. A depleted `DISABLE` weapon becomes usable as soon as its damage falls below `Max_Damage`.

## Durability from breaking blocks

The Minecraft `Tool` component may also damage a weapon when it breaks a matching block:

```yaml
  Info:
    Weapon_Item:
      Tool:
        Default_Mining_Speed: 1.0
        Damage_Per_Block: 5
        Rules:
          - "#minecraft:mineable/pickaxe 4.0 true"

    Cancel:
      Break_Blocks: false
```

`Damage_Per_Block` uses the same `BREAK` or `DISABLE` behavior as shooting.

{% hint style="warning" %}
Tool components are stored on the generated item. After changing `Damage_Per_Block` or its rules, obtain a new copy of the weapon before testing.
{% endhint %}

## Complete example

```yaml
Example_Weapon:
  Info:
    Weapon_Item:
      Type: "IRON_HOE"
      Name: "<gold>Durability Test Weapon"
      Durability:
        Max_Damage: 1000
        Damage: 0
      Tool:
        Default_Mining_Speed: 1.0
        Damage_Per_Block: 5
        Rules:
          - "#minecraft:mineable/pickaxe 4.0 true"

    Durability:
      On_Depleted: DISABLE

    Weapon_Break_Mechanics:
      - "Sound{sound=entity.item.break}"
      - "Message{message=<red>Your weapon broke!}"

    Weapon_Depleted_Mechanics:
      - "Sound{sound=entity.item.break}"
      - "Message{message=<red>Your weapon requires repairs.}"

    Cancel:
      Break_Blocks: false

  Shoot:
    Durability_Per_Shot: 25

  Repair:
    Allowed_Kits:
      - Basic_Repair_Kit
      - Advanced_Repair_Kit
```
