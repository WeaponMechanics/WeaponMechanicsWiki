---
description: Customize how the projectile flies and interacts
---

# Projectile

This section defines how your projectile moves and interacts with the environment. Remember that your projectiles are not actual entities. Instead, WeaponMechanics uses math and ray-tracing to simulate the position/movement of the projectile.

```yaml
  Projectile: <path to another Projectile>
    Projectile_Settings:
      Type: <ProjectileType>  # an entity type, or "invisible"
      Projectile_Item_Or_Block:
        Type: <Material>
        Durability: <durability>
        Unbreakable: <true/false>
        Custom_Model_Data: <custom model data number>
        Skull:
          Owning_Player: <UUID of player or name of player>
        Potion:
          Color: <ColorType>
      Gravity: <gravity>
      Minimum:
        Speed: <minimum speed of projectile>
        Remove_Projectile_On_Speed_Reached: <true/false>
      Maximum:
        Speed: <maximum speed of projectile>
        Remove_Projectile_On_Speed_Reached: <true/false>
      Drag:
        Base: <multiplier>
        In_Water: <multiplier>
        When_Raining_Or_Snowing: <multiplier>
      Disable_Entity_Collisions: <true/false>
      Maximum_Alive_Ticks: <ticks>
      Maximum_Travel_Distance: <distance>
      Size: <projectile size>
    Sticky:  # Scroll down for more info
    Bouncy:  # Scroll down for more info
    Through:  # Scroll down for more info
    Mechanics: <Mechanics>
```

#### **Projectile: \<path to another Projectile>**

Usually, you define projectiles in the `projectiles` folder, that way you can re-use the projectile in multiple weapons. For example, in this config, `my_weapon` and `my_other_weapon` both use `my_projectile` for their projectile. This saves you time, so you don't have to type things over.

```yaml
# This goes in the weapons folder
my_weapon:
  Projectile: "my_projectile.Projectile"
  Shoot: <shoot configurations>
  Reload: <reload configurations>
  <etc.>

my_other_weapon:
  Projectile: "my_projectile.Projectile"
  Shoot: <shoot configurations>
  Reload: <reload configurations>
  <etc.>

# This goes in the projectiles folders
my_projectile:
  Projectile:
    Projectile_Settings: ...
    Sticky: ...
    <etc.>
```

#### Type

Which entity does the projectile look like? It can look like an arrow, a snowball, a fireball, an end dragon, or any kind of entity type you want. Projectiles can also be hidden by using `"invisible"` for this option (This helps save some CPU performance). Use an [entity](https://app.gitbook.com/s/IIUkVnlH40vVBzLhWWQ8/references#entity "mention") for the projectile (or `"invisible"`).&#x20;

#### Projectile\_Item\_Or\_Block

Some entities can use an item for extra data. A `DROPPED_ITEM` _**requires**_ it to determine which item to drop. `FALLING_BLOCK` _**requires**_ it to determine which block to use. `ARMOR_STAND` will add any item here on it's head. The armor stand is very useful for showing custom ammo models, like a rocket for an RPG.

Use the [Item Serializer](https://app.gitbook.com/s/IIUkVnlH40vVBzLhWWQ8/item-serializer "mention") for all options.

{% hint style="info" %}
Since this uses the [Item Serializer](https://app.gitbook.com/s/IIUkVnlH40vVBzLhWWQ8/item-serializer "mention"), you can use the `Custom_Model_Data` in your projectiles, like this:

```yaml
my_projectile:
  Projectile:
    Projectile_Settings:
      Type: DROPPED_ITEM
      Projectile_Item_Or_Block:
        Type: IRON_NUGGET
        Custom_Model_Data: 10 
```
{% endhint %}

#### Gravity

This defines vertical acceleration. Positive numbers make the projectile fall down over time, and negative numbers make the projectile float up over time. The numbers are in `blocks/second^2`. Vanilla Minecraft uses `10` here. Earth's gravity is about `9.8`, and the Moon's gravity is about `1.62`. Using `0` will make the projectile "float" in a straight line.

#### Minimum

* `Speed`
  * The minimum speed the projectile can travel at.
* `Remove_Projectile`
  * Whether to remove the projectile when the minimum speed is reached.
  * true = The projectile will be removed when the minimum speed is reached.

#### Maximum

* `Speed`:
  * The maximum speed the projectile can travel at.
* `Remove_Projectile`:
  * Whether to remove the projectile when the maximum speed is reached.

#### Drag

Drag allows you to multiply projectile velocity by a number every tick. Since we want the projectile to slow down, we should use a number between `0.0` and `1.0` (But you probably want to keep this between `0.9` and `1.0`, otherwise the projectile may slow down too quickly). Using exactly `1.0` will keep speed constant, and using any number above `1.0` will increase speed over time.

* `Base`
  * The amount to multiply the speed by every tick.
* `In_Water`
  * The amount to multiply the speed by when the projectile is in liquid.
* `When_Raining_Or_Snowing`
  * The amount to multiply the speed by when it is raining or snowing.

{% hint style="danger" %}
You cannot use negative numbers for drag. To slow the projectile down, use a positive number <1, like `0.98`. To speed the projectile up like a rocket, use a positive number >1, like `1.03`.&#x20;
{% endhint %}

#### Disable\_Entity\_Collisions

Setting this to `true` will stop the projectile from colliding with entities. This is useful for providing a CPU performance boost to your projectile, but it will disable all entity interacts.

{% hint style="warning" %}
Using this feature disables all entity interactions, including [#sticky](./#sticky "mention"), [#bouncy](./#bouncy "mention"), [#through](./#through "mention"), and direct damage. This feature should probably only be used for grenades, since they do not need to hit entities.&#x20;
{% endhint %}

#### Maximum\_Alive\_Ticks

Defines the maximum amount of time, in ticks, in which projectile can be alive.\
Defaults to `600` which is equal to `30` seconds.

#### Maximum\_Travel\_Distance

Defines the maximum amount of distance this projectile can travel before being removed.

#### Size

Defines the size of projectile that is used for hit detection. This size is added to each direction. Meaning `0.5` is same as 1x1x1 in size. Important note about using this is that, this only works for entities and NOT for blocks.\
Defaults to `0.1`. As an example `arrow` and `snowball` have this set to `0.3` in vanilla.

#### Sticky

Use the [sticky.md](sticky.md "mention") wiki page.

#### Bouncy

Use the [bouncy.md](bouncy.md "mention") wiki page.

#### Through

Use the [#through](./#through "mention") wiki page.

#### Mechanics:

Casts mechanics to projectile's location. Useful when you want to make beeping for a grenade.\
Use [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention").&#x20;
