---
description: How the weapon should launch projectiles
---

# Shoot

{% hint style="danger" %}
The `Shoot:` module is required for all weapons
{% endhint %}

{% hint style="info" %}
`Shoot:` can be misleading; Weapons **are not required** to shoot projectiles. Instead, you can create consumables. Check out the consumable example below:

<details>

<summary>Consumable Example</summary>

This "weapon" doesn't launch a projectile. Instead, it deletes itself when used and heals the player!

```yaml
Stim:
  Info:
    Weapon_Item:
      Type: "LIGHTNING_ROD"
      Name: "<gold>Stim"
      Lore:
        - "<gray>Military stimulant that cauterizes combat wounds."
        - ""
        - "<gray>Weapon Statistics"
        - "<gold>➣ &c♥♥♥♥♥♥♥♥ <gold>⟸ <gray>Heal"
      Unbreakable: true
      Hide_Flags: true
      Deny_Use_In_Crafting: true
    Weapon_Get_Mechanics:
      - "Sound{sound=ITEM_ARMOR_EQUIP_CHAIN, pitch=0.75}"
    Cancel:
      Block_Interactions: true
      Item_Interactions: true
  Skin:
    Default:
      Type: FEATHER
      Custom_Model_Data: -1  # negative numbers are ok here!
  Shoot:
    Trigger:
      Main_Hand: "RIGHT_CLICK"
      Off_Hand: "RIGHT_CLICK"
      Circumstance:
        Swimming: "DENY"
    Consume_Item_On_Shoot: true
    Delay_Between_Shots: 20
    Mechanics:
      - "Sound{sound=ENTITY_GENERIC_DRINK, noise=0.1}"
      - "Potion{potion=HEAL, level=3}"
```

</details>
{% endhint %}

```yaml
  Shoot:
    Trigger: <Trigger>
    Projectile_Speed: <speed>
    Projectiles_Per_Shot: <amount>
    Selective_Fire:
      Trigger: <Trigger>
      Default: <SINGLE/BURST/AUTO>
      Mechanics: <MechanicsSerializer>
    Delay_Between_Shots: <ticks>
    Fully_Automatic_Shots_Per_Second: <amount>
    Burst:
      Shots_Per_Burst: <amount>
      Ticks_Between_Each_Shot: <ticks>
    Consume_Item_On_Shoot: <true/false>
    Destroy_When_Empty: <true/false>
    Ammo_Per_Shot: <amount>
    Reset_Fall_Distance: <true/false>
    Spread:  # Scroll down for more information
    Recoil:  # Scroll down for more information
    Mechanics: <Mechanics>
    Custom_Durability:  # Scroll down for more information 
    Attract_Mobs:  # Scroll down for more information, WMP feature
```

#### Trigger

The [trigger.md](../../trigger.md "mention") to use when shooting the weapon.&#x20;

{% hint style="danger" %}
Due to Minecraft limitation, using `left_click` to shoot does not work. Use `right_click` instead.&#x20;
{% endhint %}

#### Projectile\_Speed

The speed, in $$\frac{m}{s}$$, to launch the projectile at. A realistic number would be about `1000`, but we recommend around `100`.

{% hint style="danger" %}
Due to a Minecaft limitation, projectile speeds over `80.0` will appear to "drift" away from the center. For speeds above `80.0`, you should use invisible projectiles and WeaponMechanicsCosmetics to display the projectile using Trails instead.
{% endhint %}

#### Projectiles\_Per\_Shot

The number of projectiles to shoot for every shot. This is mainly used for shotguns.

#### Selective\_Fire

Selective fire lets players switch between single, burst, and full auto.&#x20;

* `Trigger` -> The [trigger.md](../../trigger.md "mention") used to switch fire modes.
* `Default` -> Either `SINGLE`, `BURST`, or `AUTO`.
* `Mechanics` -> The mechanics triggered when switching firemodes.
  * `@Source{}` -> The entity holding the weapon.

#### Delay\_Between\_Shots

The time, in ticks, between weapon shots (for `SINGLE`).

#### Fully\_Automatic\_Shots\_Per\_Second

This makes your weapon a fully automatic weapon. It is recommended to use values `[1, 20]`. Numbers `>20` will cause the gun to launch multiple projectiles during the same tick. Not every fire rate is perfect since there are only 20 server ticks every second. You _shouldn't_ be able to hear the `<50` millisecond fluctuations, but here is our grading:

`Perfect`: No fluctuations of any kind.\
`Good`: Even distribution of fluctuations.

| Fire Rate | RPM  |  Rating |
| --------- | ---- | :-----: |
| 1         | 60   | Perfect |
| 2         | 120  | Perfect |
| 3         | 180  |         |
| 4         | 240  | Perfect |
| 5         | 300  | Perfect |
| 6         | 360  |         |
| 7         | 420  |         |
| 8         | 480  |         |
| 9         | 540  |         |
| 10        | 600  | Perfect |
| 11        | 660  |         |
| 12        | 720  |         |
| 13        | 780  |         |
| 14        | 840  |         |
| 15        | 900  |   Good  |
| 16        | 960  |   Good  |
| 17        | 1020 |         |
| 18        | 1080 |   Good  |
| 19        | 1140 |   Good  |
| 20        | 1200 |   Good  |

#### Burst

* `Shots_Per_Burst` -> How many shots to fire per shot.
* `Ticks_Between_Each_Shot` -> The time, in ticks, between shots.&#x20;

#### Consume\_Item\_On\_Shoot

Use `true` to delete the weapon after a shot. This is used for consumables and grenades.&#x20;

#### Destroy\_When\_Empty

Use `true` to delete the weapon when the magazine reaches 0. This is used for special 1-time-use guns.&#x20;

#### Ammo\_Per\_Shot

How much ammo to consume per shot.&#x20;

#### Reset\_Fall\_Distance

Resets the fall distance after shooting so the entity doesn't take fall damage (unless they continue to fall). Great for jet-packs or rocket boosts.&#x20;

#### Spread

Check out the [spread.md](spread.md "mention") wiki page.

#### Recoil

Check out the [recoil.md](recoil.md "mention") wiki page.

#### Mechanics

Mechanics triggered when shooting. Use the [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") wiki.&#x20;

* `@Source{}` -> The entity shooting the gun.

#### Custom\_Durability

Check out the [#custom\_durability](./#custom\_durability "mention") wiki page.&#x20;

#### Attract\_Mobs

{% hint style="warning" %}
This is a WeaponMechanicsPlus feature. You need to purchase it before you can use the `Attract_Mobs` feature.
{% endhint %}

Allows you to attract creatures to your location. This is great for zombie survival servers, since you can alert all zombies in a radius to attack the shooter.

```yaml
  Shoot:
    Attract_Mobs:  # This has to go in the "Shoot" section
      Skip_Chance: 50%
      Default_Mode: <CANCEL/ATTRACT>
      Default_Distance: <distance>
      Default_Chance: 100%
      Default_Override_Current_Target: <true/false>
      Mobs:
        - <mob*> <CANCEL/ATTRACT*> <distance> <chance> <override current target>
      Mechanics: <Mechanics>
```

* `Skip_Chance` -> If this is `75%`, then there is a 75% chance that we will skip all attract mob calculations, and no mobs will be attracted. This is primarily done for performance. Defaults to `0%`.
* `Default_Mode` -> Use `ATTRACT` to attract ALL mobs by default.
* `Default_Distance` -> The default distance to attract all mobs from. Distance is measured in blocks. Defaults to `40.0`.&#x20;
* `Default_Chance` -> The chance to attract that specific mob. This is mainly useful to "stagger" the number of mobs that are attracted at once. Defaults to `100%`.
* `Default_Override_Current_Target` -> Use `true` to override the current mob's target. Defaults to `false`.
* `Mobs` -> The mob list for specific entity configurations.
* `Mechanics` -> The mechanics to play whenever a mob targets you.

**Example:**

<pre class="language-yaml"><code class="lang-yaml"><strong>  Shoot:
</strong><strong>    # This example will attract all zombies in a 60 block radius,
</strong><strong>    # regardless whether or not you are wearing a zombie head. When
</strong><strong>    # a zombie is initially targeted to you, they will recieve a 6
</strong><strong>    # second speed boost. This is enough for them to catch up to you.
</strong>    Attract_Mobs:
      Mobs:
        - ZOMBIE ATTRACT 60.0 100%
      Mechanics:
        - "Potion{potion=SPEED, level=3, time=120} @Target{}"
</code></pre>
