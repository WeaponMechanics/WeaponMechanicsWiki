---
description: Add consumable ammunition to your guns
---

# Ammo

If you want to prevent players from shooting guns forever, you should use `Ammo`. Ammo is split into 2 sections, the [#weapon-config](ammo.md#weapon-config "mention") and the [#ammo-config](ammo.md#ammo-config "mention").&#x20;

## Weapon Config

```yaml
<weapon>:
  Reload: # Make sure that the Ammo section is INSIDE the Reload section!
    Ammo: 
      Out_Of_Ammo_Mechanics: <Mechanics>
      Ammo_Switch_Trigger: <Trigger>
      Ammo_Switch_Mechanics: 
      Ammos:
        - <ammo1>
        - <ammo2>
```

#### Out\_Of\_Ammo\_Mechanics

The mechanics triggered when the player tries to shoot but the weapon is empty. Use the [Mechanics](http://127.0.0.1:5000/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") wiki.&#x20;

* `@Source{}` -> The player who tried to shoot.

#### Ammo\_Switch\_Trigger

The [trigger.md](../../trigger.md "mention") that is used to switch between ammo types. Typically, you use `SWAP_HANDS`. For example:

```yaml
      Ammo_Switch_Trigger:
        Main_Hand: SWAP_HANDS
        Off_Hand: SWAP_HANDS
```

#### Ammo\_Switch\_Mechanics

The mechanics triggered when you swap ammo types (So, right after the [#ammo\_switch\_trigger](ammo.md#ammo\_switch\_trigger "mention") is used).

#### Ammos

A list of all ammunition that this weapon can use. A typical server will only have 1 ammunition per gun. However, if you purchase WeaponMechanicsPlus, then you can make explosive ammo, fire ammo, and much more!

For example:

```yaml
      Ammos:
        - Rocket  # This Rocket is defined in the Ammo Config (see below)
```

## Ammo Config

So where does the ammo config go? Not in the weapon files! Instead, go to <mark style="color:yellow;">**yourserver -> plugins -> WeaponMechanics -> ammos**</mark> and create a new `.yml` file (Or use the default one).&#x20;

Make sure you replace `<ammo_title>` with a unique name for your ammo, and do not use any special characters. For example, `.50` will not work but `50_Caliber` is good.&#x20;

```yaml
<ammo_title>:
  Symbol: <string>
  Experience_As_Ammo_Cost: <amount>
  Money_As_Ammo_Cost: <amount>
  Item_Ammo:
    Bullet_Item: <Item>
    Magazine_Item: <Item>
    Ammo_Converter_Check:
      Type: <true/false>
      Name: <true/false>
      Lore: <true/false>
      Enchantments: <true/false>
```

#### Symbol

This is what is displayed by the `<ammo_type>` placeholder in your [#weapon\_info\_display](../info.md#weapon\_info\_display "mention"). If you do not use any Symbol, it defaults to the ammo title.&#x20;

#### Experience\_As\_Ammo\_Cost

Consumes experience points (not levels) to load your gun. Most mobs drop 5 experience points.&#x20;

#### Money\_As\_Ammo\_Cost

If you have Vault installed, you can consume currency to load your gun.&#x20;

#### Item\_Ammo

Consumes items to be used as ammo. You can use one of `Bullet_Item` or `Magazine_Item`, or you can use **both**.&#x20;

* `Bullet_Item`
  * The item for individual bullets.
  * Uses the [Item Serializer](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/item-serializer "mention").
* `Magazine_Item`&#x20;
  * The item for full magazines to load into the gun.
  * Uses the [Item Serializer](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/item-serializer "mention").
* `Ammo_Converter_Check`
  * (_Optional_)
  * Converts vanilla items into ammo usable by WeaponMechanics automatically.
  * For example, `Type: true` will convert all items of the same material to usable ammo.&#x20;
