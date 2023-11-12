---
description: Break weapons over time + Repair kits
---

# Custom Durability

Custom durability can be used to make guns wear down over time, and eventually break completely. This prevents users from using the same weapon forever (Good for open-world servers).

```yaml
    Custom_Durability:
      Max_Durability: <Integer>
      Lose_Max_Durability_Per_Repair: <Integer>
      Min_Max_Durability: <Integer>
      Durability_Per_Shot: <Integer>
      Chance_To_Lose: <Chance>
      Broken_Item: <ItemSerializer>
      Lose_Durability_Mechanics: <Mechanics>
      Break_Mechanics: <Mechanics>
      
      # OPTIONAL REPAIR MODULES
      Repair_Items:
        Repair_Item_1: 
          Item: <ItemSerializer>
          Repair_Amount: <Integer>
        Repair_Item_2: 
          Item: <ItemSerializer>
          Repair_Amount: <Integer>
      Repair_Per_Exp: <Integer>
      Repair_Mechanics: <Mechanics>
      Deny_Repair_Mechanics: <Mechanics>
```

<details>

<summary>Example</summary>

This is a "test" example for you to play around with:

```yaml
    Custom_Durability:
      Max_Durability: 1000
      Min_Max_Durability: 0
      Lose_Max_Durability_Per_Repair: 100
      Durability_Per_Shot: 1
      Chance_To_Lose: 100%
      Broken_Item: 
        Type: IRON_SHOVEL
        Name: "<red>Broken AK-47"
      Break_Mechanics:
        - "Sound{sound=ENTITY_ITEM_BREAK}"
      Repair_Mechanics:
        - "Sound{sound=BLOCK_ANVIL_USE}"
      Deny_Repair_Mechanics:
        - "Sound{sound=ENTITY_VILLAGER_NO}"
        - "ActionBar{message=<red>Cannot repair item any more}"
      Repair_Per_Exp: 1
      Repair_Items:
        Item_1:
          Item: RED_WOOL
          Repair_Amount: 300
```

</details>

#### Max\_Durability

The maximum durability the weapon can have. This is also the _starting durability_ of the weapon.&#x20;

#### Lose\_Max\_Durability\_Per\_Repair

Maybe you want weapons to be repairable, **BUT** you do not want players to keep the same weapon forever. This option allows you to decrease the maximum durability over time.

Every time you use a [#repair-kit](custom-durability.md#repair-kit "mention") or a [#repair\_items](custom-durability.md#repair\_items "mention") on this weapon, the max durability will be reduced.&#x20;

#### Min\_Max\_Durability

The minimum value of `Max_Durability`. This means that after you constantly repair the weapon over and over, the `Max_Durability` will never fall below this value.

This defaults to `0`, which causes the weapon to completely break when it is repaired too many times.&#x20;

#### Durability\_Per\_Shot

How much durability to consume every shot. Defaults to `1`.

#### Chance\_To\_Lose

The percentage chance to lose durability each shot. Defaults to `100%`.&#x20;

#### Broken\_Item

If you delete this line, when the weapon is broken it is gone forever (Just like vanilla Minecraft tools/weapons/armor; they break).&#x20;

If you use this option, when the weapon breaks, it will be _"transformed"_ into this item. This item cannot shoot/reload/scope, but it _CAN_ be repaired back into a working weapon.&#x20;

Uses [Item Serializer](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/item-serializer "mention").

#### Lose\_Durability\_Mechanics

Mechanics triggered after losing durability. Uses [Mechanics](http://127.0.0.1:5000/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention").&#x20;

* `@Source{}` -> The entity holding the damaged weapon.

#### Break\_Mechanics

Mechanics triggered after the weapon breaks. Use [Mechanics](http://127.0.0.1:5000/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention"). You probably want to use the `ENTITY_ITEM_BREAK` sound.&#x20;

#### Repair\_Items

Items that can be used to repair the weapon. Think of these as "parts" that you can drag and drop onto your weapon to repair it.&#x20;

* `Item` -> The item used for repairing. Uses [Item Serializer](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/item-serializer "mention").
* `Repair_Amount` -> How much durability to repair.&#x20;

{% hint style="info" %}
`Repair_Items` and Repair Kits are 2 different things. `Repair_Items` are defined _per weapon_. 1 repair kit can be used for all weapons.
{% endhint %}

#### Repair\_Per\_Exp

Like the mending enchantment, this repairs durability while you hold the weapon and pickup experience orbs.&#x20;

{% hint style="warning" %}
Using the `/exp` command will not repair your weapon. You must pick up experience orbs.
{% endhint %}

#### Repair\_Mechanics

Mechanics triggered when the weapon is repaired by a repair item/kit. Uses [Mechanics](http://127.0.0.1:5000/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention"). Consider playing the `BLOCK_ANVIL_USE` sound.

* `@Source{}` -> The entity repairing the weapon.&#x20;

#### Deny\_Repair\_Mechanics

Mechanics triggered when the player attempts to repair a weapon but it is already fully repaired. Uses [Mechanics](http://127.0.0.1:5000/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention").

* `@Source{}` -> The entity repairing the weapon.

## Repair Kit

Repair kits are defined in the <mark style="color:yellow;">**your server -> plugins -> WeaponMechanics -> repair\_kits**</mark> folder.&#x20;

```yaml
<kit_name>:
  Total_Durability: <Integer>
  Override_Max_Durability_Loss: <Integer>
  Consume_On_Use: <true/false>
  Blacklist: <true/false>
  Weapons:
    - <weapon>
  Item: <ItemSerializer>
  Break_Mechanics: <Mechanics>
```

<details>

<summary>Example</summary>

```yaml
my_repair_kit:
  Total_Durability: 10000
  Blacklist: false
  Item:
    Type: IRON_INGOT
    Name: "<yellow>Weapon Repair Kit"
    Lore:
      - "<gray>Drag and drop this onto a weapon to repair it"
```

</details>

#### \<kit\_name>

You should choose a unique name for your repair kit that has not been used anywhere else in your files, like `My_Awesome_Repair_Kit` or `Rifle_Repair_Kit`.&#x20;

#### Total\_Durability

This is the maximum amount of durability that this Repair Kit can repair. As you use this kit more and more, this number gets lower and lower. Once this number reaches `0`, the kit is broken.

#### Override\_Max\_Durability\_Loss

If you define this option, it overrides the weapon's [#lose\_max\_durability\_per\_repair](custom-durability.md#lose\_max\_durability\_per\_repair "mention").

#### Consume\_On\_Use

Use `true` to break the repair kit after it's first usage, regardless of how much durability is used. Defaults to `false`.

#### Blacklist

If `Blacklist: true`, then any weapons on the list **CANNOT** be repaired by this repair kit. If `Blacklist: false`, then **ONLY** weapons on the list can be repaired.

#### Weapons

The list of weapon titles from WeaponMechanics. See [#blacklist](custom-durability.md#blacklist "mention") for more information.

#### Item

Uses [Item Serializer](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/item-serializer "mention").

#### Break\_Mechanics

Mechanics triggered when the repair kit breaks. Uses [Mechanics](http://127.0.0.1:5000/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention").&#x20;
