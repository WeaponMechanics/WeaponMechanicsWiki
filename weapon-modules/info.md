---
description: Basic info about your weapon visual appearance
---

# Info

{% hint style="danger" %}
The `Info:` module is required for all weapons
{% endhint %}

```yaml
  Info:
    Weapon_Item: <Item Serializer>
    Weapon_Info_Display: # scroll down for more information
    Dual_Wield: # scroll down for more information
    Weapon_Converter_Check:
      Type: <true/false>
      Name: <true/false>
      Lore: <true/false>
      Enchants: <true/false>
    Weapon_Get_Mechanics: <Mechanics>
    Weapon_Equip_Mechanics: <Mechanics>
    Weapon_Equip_Delay: <ticks>
    Weapon_Holster_Mechanics: <Mechanics>
    Cancel:
      Block_Interactions: <true/false>
      Item_Interactions: <true/false>
      Break_Blocks: <true/false>
      Drop_Item: <true/false>
      Swap_Hands: <true/false>
      Arm_Swing_Animation: <true/false>
```

#### Weapon\_Item

The item to use as the weapon. Uses the [Item Serializer](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/item-serializer "mention"). This is also where you define lore, attributes, etc.

#### Weapon\_Info\_Display

How to show ammo and other information in the action bar. Uses placeholders and colors. Check out the default weapons for examples.&#x20;

<details>

<summary>Display Example</summary>

```yaml
    Weapon_Info_Display:
      Action_Bar:
        Message: "<gold>AK-47<firearm_state> <gray>«<gold><ammo_left><gray>»<gold><reload>"
```

</details>

```yaml
    Weapon_Info_Display:
      Action_Bar:
        Message: <string>
        Dual_Wield:
          Main_Hand: <string>
          Off_Hand: <string>
      Boss_Bar:
        Title: <string>
        Bar_Color: <string>
        Bar_Style: <string>
        Dual_Wield:
          Main_Hand: <string>
          Off_Hand: <string>
      Show_Ammo_In:
        Boss_Bar_Progress: <true/false>
        Exp_Level: <true/false>
        Exp_Progress: <true/false>
```

#### Dual\_Wield

Dual-wielding with weapons is always disabled by default. If you want to be able to shoot with both hands at the same time, you'll have to add dual wielding for both weapons while allowing them to dual wield with each other.

Only the other hand may reload the weapon at a time and only other weapon may apply zooming. Both weapons can still shoot simultaneously.

<details>

<summary>50_GS Dual Wield Example</summary>

```yaml
    Dual_Wield:
      Whitelist: true
      Weapons:
        - "50_GS"
```

</details>

```yaml
    Dual_Wield:
      Whitelist: <true/false>
      Weapons:
      - <weapon title>
      - <etc.>
      Mechanics_On_Deny: <Mechanics>
```

* `Whitelist`
  * Whether to use `Weapons` as a whitelist or blacklist.
    * A whitelist means that only X options are allowed to be used.
    * A blacklist means that X options are NOT allowed to be used.
  * `true` -> Only weapons listed in `Weapons` can be used.
* `Weapons`
  * List of valid weapons. You should enter the weapon titles of the guns.
  * This list's behavior changes based on the value of `Whitelist`
* `Mechanics_On_Deny`
  * These mechanics will be run when dual wielding is denied.
  * Helpful in sending denial messages and denial sounds.
  * Use the [Mechanics](http://127.0.0.1:5000/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") wiki.

#### Weapon\_Converter\_Check

For a regular item to become a "weapon," WeaponMechanics checks if the item should become a weapon. This is the list of checks the plugin goes through to determine if it should convert an item into a weapon. This is especially useful if you want players to get weapons through "vanilla means," like trading.

* `Type`
  * Check if the material of the item is the same.
  * Material Examples: `stone`, `stick`, `emerald`.
* `Name`
  * Check if the name of the item is the same.
  * Note: If your weapon name has a color (e.g., `"<yellow>AK-47"`), then the item must have that color.
  * Note: These 2 options are **NOT** equal `"<yellow><yellow>M4A1" ≠ "<yellow>M4A1"`.
* `Lore`
  * Check if the lore of the item is the same.
  * Enable this if you want _COMPLETE CONTROL_ over who gets weapons since regular players cannot give lore to items.
* `Enchants`
  * Check if the enchantments of the item are the same.
  * Note: Check both the enchantments _AND_ the levels.

#### Weapon\_Get\_Mechanics

Mechanics triggered when getting the weapon through command (`/wm give`)

* `@Source{}` -> The entity being given the weapon.

#### Weapon\_Equip\_Mechanics

Mechanics triggered when equipping the weapon in hand.

* `@Source{}` -> The entity holding the weapon

#### Weapon\_Equip\_Delay

The time, in ticks, after equipping the weapon before it can be shot. This prevents players from switching weapons too quickly to get an unfair advantage. Sidearms should have a lower equip delay then primaries.&#x20;

#### Weapon\_Holster\_Mechanics

Mechanics triggered when holstering the weapon (taking it out of your hand).

* `@Source{}` -> The entity holding the weapon

#### Cancel

Cancels certain events while holding the weapon.&#x20;

* `Block_Interactions`&#x20;
  * Cancels opening doors, chests, etc.
  * This causes the item to bob up and down; _you should not use this_.
* `Item_Interactions`
  * Cancels tilling dirt, shearing logs, etc.
  * This causes the item to bob up and down; _you should not use this_.
* `Break_Blocks`
  * Cancels breaking blocks.
* `Drop_Item`
  * Cancels dropping the gun while holding it.
* `Swap_Hands`
  * Cancels swapping hands between main hand and off hand (Pressing `F`).
* `Arm_Swing_Animation`
  * Cancels arm swing animation for other players (Like the punch animation).&#x20;

{% hint style="warning" %}
Due to visual item bobbing glitches, I recommend using the following configuration for all of your guns:

```yaml
    Cancel:
      Drop_Item: true
      Swap_Hands: true
      Arm_Swing_Animation: true
```
{% endhint %}
