---
description: Commonly asked questions and answers.
---

# Common Questions

#### <mark style="color:green;">How do I get ammo? How can I make guns use bullets? Why can I shoot infinitely?</mark>

If you want players to load their guns with item bullets, you must configure an [ammo.md](weapon-modules/reload/ammo.md "mention") section for each gun you want. After configuring your ammo, you can use the `/wm ammo` command.

***

#### <mark style="color:green;">How do I get the resource pack?</mark>

The resource pack is automatically downloaded to the <mark style="color:yellow;">**your server -> plugins -> WeaponMechanics**</mark> folder. Alternatively, you can check the [latest release](https://github.com/WeaponMechanics/MechanicsMain/releases). We also have a [version history](https://github.com/WeaponMechanics/MechanicsMain/tree/master/resourcepack) of the resource pack.

***

#### <mark style="color:green;">Does WeaponMechanics support Bedrock (GeyserMC)?</mark>

WeaponMechanics, as a plugin, fully supports bedrock (the guns shoot, reload, scope, etc.). However, the resource pack used by WeaponMechanics is not built for Bedrock. You will have to create your resource pack.

***

#### <mark style="color:green;">The shooting sounds are super loud; can I turn them down?</mark>

Yes! By default, we included 3 different volumes in the resource pack: `.loud`, `.ambient`, and `.quiet`. To reduce the volume, you must go into each weapon file and replace the `.loud` with `.ambient`. I recommend using a search and replace (`ctrl + f`).&#x20;

***

#### <mark style="color:green;">Is WeaponMechanics free?</mark>

WeaponMechanics is [free to download](https://github.com/WeaponMechanics/MechanicsMain/releases) and [open source](https://github.com/WeaponMechanics/MechanicsMain) for contributions! However, we do have add-ons that cost money. Want to support my continued development? Consider purchasing:

1. BiomeManager -> Paint biomes different colors (with particle effects and more)!
2. WeaponMechanicsCosmetics -> Cosmetic additions to your guns, including sounds, particles, and skins!
3. WeaponMechanicsPlus -> Add attachments and modifiers to your guns for a dynamic and in-depth system!

***

#### <mark style="color:green;">Why can't my weapons break blocks in WorldGuard regions?</mark>

WeaponMechanics has full WorldGuard support. Check out [#worldguard](addons.md#worldguard "mention") for more information.

If you cannot break blocks in a region, or you receive the message:

> <mark style="color:red;">**Hey!**</mark> Sorry, but you can't break that block here.

That means you should go into <mark style="color:yellow;">**yourserver -> plugins -> WeaponMechanics -> config.yml**</mark> and set these options to `true`:

```yaml
Disable_Entity_Explode_Event: true  # change this to true
Disable_Block_Break_Event: true  # change this to true
```

