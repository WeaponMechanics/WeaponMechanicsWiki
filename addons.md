---
description: Features with other plugins
---

# Addons

## Plugins

1. [#weaponmechanicscosmetics](addons.md#weaponmechanicscosmetics "mention")
2. [#weaponmechanicsplus](addons.md#weaponmechanicsplus "mention")
3. [#armormechanics](addons.md#armormechanics "mention")
4. [#damagemechanics](addons.md#damagemechanics "mention")
5. [#mythicmobs](addons.md#mythicmobs "mention")
6. [#worldguard](addons.md#worldguard "mention")
7. [#vivecraftspigotextensions](addons.md#vivecraftspigotextensions "mention")

### WeaponMechanicsCosmetics

Adds cosmetic effects, like bullet impact sounds, 3D bullet "zip" feedback, trails, skins, impact particles, muzzle flashes, pumpkin scope zooms, shaped particle effects, and more! WeaponMechanicsCosmetics is a paid addon, which can be purchased on Spigot.

***

### WeaponMechanicsPlus

Adds attachment modifiers to your weapons. Upgrade your weapons with craftable attachments, unlocking infinite possibilities for your guns. WeaponMechanicsPlus also adds armor attachments for ArmorMechanics, and new weapon modules:

1. [Firemode](https://app.gitbook.com/s/9hOjsLnIiB5Xm8MOXgWU/firemode "mention")&#x20;

WeaponMechanicsPlus is a paid plugin that cannot be purchased now (Will be purchasable later).&#x20;

***

### ArmorMechanics

Armor set and special effects plugin with full WeaponMechanics support. You can add set bonuses, make armor resistant to WeaponMechanics explosions and bullets, and much more!

***

### DamageMechanics

A standalone plugin that lets you modify damage multipliers. Great for gun servers that want to change the health of players (Like 20 -> 100). This plugin lets you multiply damage (triple fire tick damage, for example) and regeneration (regenerate 5 hearts instead of half a heart, for example).

***

### MythicMobs

[MythicMobs](https://www.spigotmc.org/resources/5702/) is a plugin that allows you to create custom creatures with abilities. WeaponMechanics adds `weaponMechanicsShoot`, which effectively allows creatures to shoot guns! For more information on how to use skills, check out the [MythicMobs wiki](https://git.mythiccraft.io/mythiccraft/MythicMobs/-/wikis/Skills/Start).

Note that mobs cannot reload, scope, sneak, etc. Instead, each shot is simulated as the "first shot" from a magazine.

**`weaponMechanicsShoot` (**[**Skill**](https://git.mythiccraft.io/mythiccraft/MythicMobs/-/wikis/Skills/Start)**)**

| Attribute   | Alias  | Description                                                    | Default         |
| ----------- | ------ | -------------------------------------------------------------- | --------------- |
| weaponTitle | weapon | The weapon title (from config) of the weapon to shoot          | None (Required) |
| spread      |        | The angle (in degrees) of the maximum random spread            | 0.0             |
| head        |        | true to aim at the target's head (false to aim for the center) | true            |



**`weaponMechanicsWeapon` (**[**Item**](https://git.mythiccraft.io/mythiccraft/MythicMobs/-/wikis/Mobs/Equipment)**)**

| Attribute   | Alias  | Description                                           | Default         |
| ----------- | ------ | ----------------------------------------------------- | --------------- |
| weaponTitle | weapon | The weapon title (from config) of the weapon to equip | None (Required) |
| amount      | a      | The number of weapons to equip                        | 1               |



**`weaponMechanicsArmed` (**[**Condition**](https://git.mythiccraft.io/mythiccraft/MythicMobs/-/wikis/Skills/conditions)**)**

Checks if the target is holding a weapon. You can check for specific weapons, like `AK-47,RPG-7,Tactical_Knife`, or use `*` for any weapon.

| Attribute | Alias | Description                                         | Default |
| --------- | ----- | --------------------------------------------------- | ------- |
| weapons   |       | The weapons to check for, or use `*` for any weapon | \*      |



**`weaponMechanicsReloading` (**[**Condition**](https://git.mythiccraft.io/mythiccraft/MythicMobs/-/wikis/Skills/conditions)**)**

Check if the target is currently reloading. Doesn't have any config options.

Here is an example:

```yaml
Gunner:
  Type: zombie
  Display: '&aGunner'
  Health: 40
  Damage: 0.1
  Equipment:
  # Hold an AK_47 (THIS IS NOT REQUIRED TO SHOOT THE AK)
  - weaponMechanicsWeapon{weapon=AK_47} HAND
  Skills:
  # This example will shoot 5 ak_47 projectiles towards the target's
  # head (give or take 12 degrees in any direction).
  - weaponMechanicsShoot{weapon=AK_47;spread=12;head=true;repeat=5;repeatInterval=1} @Target ~onTimer:80
  # This example will shoot a cluster grenade at all players every 20 seconds
  - weaponMechanicsShoot{weapon=Cluster_Grenade;spread=30;head=false} @PIR{r=20} ~onTimer:400
```

***

### WorldGuard

[WorldGuard](https://dev.bukkit.org/projects/worldguard) is a plugin that allows you to form regions. In these regions, you add flags to add functionality. Using these flags allow you to prevent griefers from destroying builds and/or damaging players.

* **`weapon-shoot` ->** Prevents shooting weapons
* **`weapon-shoot-message` ->** Message sent to the shooter when denied
* **`weapon-explode` ->** Prevents explosions caused by weapons
* **`weapon-explode-message` ->** Message sent to the shooter when denied
* **`weapon-break-block` ->** Prevents block damage (By either explosions or WMC block damage)
* **`weapon-damage` ->** Prevents damaging entities with weapons
* **`weapon-damage-message` ->** Message sent to the shooter when denied

***

### VivecraftSpigotExtensions

A standalone plugin that lets VR users join the server. Note that the original plugin should never be used with WeaponMechanics. Instead, [use our remake](https://www.spigotmc.org/resources/vivecraft-spigot-extensions-remake.111303/).

{% hint style="warning" %}
By default, the VR players will see guns from the resource pack _backward_ and offset from the hand. All VR players must enable custom item data in controller settings.&#x20;
{% endhint %}

***
