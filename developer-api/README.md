---
description: Developer API for your plugins
---

# Developer API

## Links

* [#how-it-works](./#how-it-works "mention")
* [#weaponmechanicsapi](./#weaponmechanicsapi "mention")
* [#events](./#events "mention")
* [cloning-repository.md](cloning-repository.md "mention")
* [projectile-scripts.md](projectile-scripts.md "mention")

***

## How it works

Before jumping into contributing or making your addon, you should be familiar with the "big" sections of WeaponMechanics.

#### Data Serialization

Instead of pulling values from a `YamlConfiguration` instance, WeaponMechanics stores a flattened `Map<String, Object>`, and each weapon uses probably 100 different "serializers." We coded these serializers to check for user errors, and to report them to the console immediately.&#x20;

#### Projectiles

WeaponMechanics does not use Minecraft entities. Instead, we use "fake" ray-traced projectiles. When you use a disguise like a snowball or armor stand, WeaponMechanics spawns a fake entity using packets.

#### Weapon Handlers

The "big chunks of logic" are separated into handlers, like the ShootHandler and the ReloadHandler.&#x20;

***

## WeaponMechanicsAPI

The [WeaponMechanicsAPI class](https://github.com/WeaponMechanics/WeaponMechanics/blob/master/weaponmechanics-core/src/main/java/me/deecaad/weaponmechanics/WeaponMechanicsAPI.java) is a list of easy-access examples. If you are looking for a specific method, try tracing the API calls to their source (This will help you find new methods).

{% hint style="success" %}
Want a new API method added? Submit a feature request!
{% endhint %}

**Checking if a Player is scoping/reloading/whatever**

WeaponMechanics has player wrappers. Use `WeaponMechanics.getEntityWrapper(entity)` to get a wrapper. You probably want to get `HandData` (use `IEntityWrapper#getMainHandData()` and `IEntityWrapper#getOffHandData()`).

**Generating/Giving weapon items**

The `InfoHandler` handles weapon generation. Use `WeaponMechanics.getWeaponHandler().getInfoHandler()`. It can also be used to check if an existing `ItemStack` is a WeaponMechanics weapon.

**Spawning Projectiles**

Perhaps you want to spawn in a projectile after implementing your custom projectile or using one of the premade projectile classes. While you can create your own repeating task, this becomes messy. Instead, add projectiles to the `ProjectilesRunnable` instance (Use `WeaponMechanics.getProjectilesRunnable()`) then add projectiles through that.

**Checking for block regeneration**

You probably don't want to interfere with block regeneration when working in protected regions. Or perhaps you are implementing a feature that causes block damage and want to use WeaponMechanic's premade system. Either way, look at `BlockDamageData`.

## Events

For the complete list of events, check out the [events package](https://github.com/WeaponMechanics/WeaponMechanics/tree/master/weaponmechanics-core/src/main/java/me/deecaad/weaponmechanics/weapon/weaponevents). Most events inherit from the `WeaponEvent` class.
