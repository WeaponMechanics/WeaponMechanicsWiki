---
description: Fine-tuning the damage based on conditions
---

# Damage Modifiers

Damage modifiers modify the amount of damage dealt based on my factors, like armor, enchantments, potions, movement, hit point, and entity type.

Every weapon, by default, uses the `Damage_Modifiers` section from config.yml. However, you might want your weapon to override those modifiers. Check out [#damage\_modifiers](./#damage\_modifiers "mention") from the [.](./ "mention") module.&#x20;

```yaml
  Damage_Modifiers:
    Min: 20%   
    Max: 300% 
    Per_Armor_Point: -3%
    Armor:
      - IRON_HELMET -5%
    Enchantments:
      - projectile_protection -8%
      - protection -4%

    # Modifiers for where the bullet hits the body
    Head: +50%
    Body: +0%
    Arms: -20%
    Legs: -20%
    Feet: -50%
    Back: +20%

    # Moving targets are not braced for impact
    Sneaking: -5%
    Walking: +0%
    Swimming: +5%
    Sprinting: +5%
    In_Midair: +5%

    # Player holding a shield and facing the damage direction
    Shielding: -100%

    Entities:
      - ZOMBIE +50%
      - PLAYER -50%
    Potions:
      - weakness +10%
```

#### Min

The minimum percentage of damage. `0%` means it is _possible_ for a bullet to deal 0 damage. You probably want to set this a bit higher, like `20%`.&#x20;

#### Max

The maximum percentage of damage. You should set this a bit higher then `100%`.

#### Per\_Armor\_Point

Gets the armor value of the damaged entity (includes the armor they are wearing, custom armor attributes, and per-entity armor attributes). Remember that full diamond armor is 20 armor points, so don't set this number too high (`-5%` is probably the highest you want to go).

#### Armor

A list of armor pieces and their hardcodes resistances.

{% hint style="warning" %}
This feature is hard to use correctly, so you should probably use [#per\_armor\_point](damage-modifiers.md#per\_armor\_point "mention") instead.
{% endhint %}

#### Enchantments

A list of enchantments and their modifiers. The modifier is multiplied by the enchantment level. Use the [Enchantment](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/references#enchantment "mention") list.

The following example will do 8% less damage for each projectile protection level and 5% less for each level of protection.&#x20;

```yaml
    Enchantments:
      - projectile_protection -8%
      - protection -4%
```

{% hint style="warning" %}
In `1.12.2`, the enchantments use the [old format](https://helpch.at/docs/1.12.2/org/bukkit/enchantments/Enchantment.html).
{% endhint %}

#### Head

Headshot damage modifier (headshots deal high damage?)

#### Body

Body shot damage modifier (body shots deal medium damage?)

#### Arms

Arm shot damage modifier (arm shots deal less damage?)

#### Legs

Leg shot damage modifier (leg shots deal less damage?)

#### Feet

Foot shot damage modifier (foot shots do minor damage?)

#### Sneaking

Modify damage if the victim is sneaking (as if they are braced for impact).

#### Walking

Modify damage if the victim is walking.

#### Swimming

Modify damage if the victim is swimming in water.

#### Sprinting

Modify damage if the victim is sprinting.

#### In\_Midair

Modify damage if the victim is in the air when damaged.&#x20;

#### Shielding

Reduce incoming damage when the victim is blocking with their shield and facing the damage.&#x20;

#### Entities

A list of [entity](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/references#entity "mention") and modifiers.&#x20;

The following example does double damage to zombies:

```yaml
    Entities:
      - zombie 100%
```

#### Potions

A list of [potion-effect](http://127.0.0.1:5000/s/IIUkVnlH40vVBzLhWWQ8/references#potion-effect "mention") and modifier.

The following example does 10% more damage to entities with weakness.

```yaml
    Potions:
      - weakness +10%
```
