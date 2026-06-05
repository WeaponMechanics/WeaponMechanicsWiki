---
description: Commonly asked questions and answers.
---

# Common Questions

#### <mark style="color:green;">How do I get ammo? How can I make guns use bullets? Why can I shoot infinitely?</mark>

If you want players to load their guns with item bullets, you must configure an [ammo.md](weapon-modules/reload/ammo.md "mention") section for each gun you want. After configuring your ammo, you can use the `/wm ammo` command.

***

#### <mark style="color:green;">How do I get the resource pack?</mark>

The resource pack is automatically downloaded to the <mark style="color:yellow;">**your server -> plugins -> WeaponMechanics**</mark> folder. Alternatively, you can check the [latest release](https://github.com/WeaponMechanics/MechanicsMain/releases).

***

#### <mark style="color:green;">Does WeaponMechanics support Bedrock (GeyserMC)?</mark>

No, only unofficially through GeyserMC. Any bugs should be reported to the authors of GeyserMC, we do not care.

***

#### <mark style="color:green;">The shooting sounds are super loud; can I turn them down?</mark>

Yes! By default, we included 3 different volumes in the resource pack: `.loud`, `.ambient`, and `.quiet`. To reduce the volume, you must go into each weapon file and replace the `.loud` with `.ambient`. I recommend using a search and replace (`ctrl + f`).

Remember that in Minecraft, volume levels past `1.0` only effect the DISTANCE at which you can hear the sound. To actually change the volume, you need to change the volume of the sound file itself using a program like audacity.&#x20;

***

#### <mark style="color:green;">Is WeaponMechanics free?</mark>

WeaponMechanics is [free to download](https://github.com/WeaponMechanics/MechanicsMain/releases) and [open source](https://github.com/WeaponMechanics/MechanicsMain) for contributions! However, we do have add-ons that cost money. Want to support my continued development? Consider purchasing:

1. WeaponMechanicsCosmetics -> Cosmetic additions to your guns, including sounds, particles, and skins!
2. WeaponMechanicsPlus -> Add attachments and modifiers to your guns for a dynamic and in-depth system!

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

***

#### <mark style="color:green;">Does WeaponMechanics support Folia?</mark>

WeaponMechanics officially supports Paper and Folia. Forks of Paper/Folia _will probably work_, but are not officially supported.

***

#### <mark style="color:green;">I don't want my guns to stack, how can I make the weapons unstackable?</mark>

You'll have to change the configs to an unstackable item, like a shovel. This means you will also have to modify the resource pack's feather.json, so the resource pack applies to the modified items.

You can also set the `Max_Stack_Size`

***

#### <mark style="color:green;">I purchased the plugin on Spigot, but Spigot is no longer updated. How can I get my license for free on Pluginify?</mark>

All updates to WeaponMechanics, ArmorMechanics, WeaponMechanicsCosmetics, WeaponMechanicsPlus, etc. are all posted to [pluginify](https://pluginify.org/) now. This is due to changes in the Spigot EULA which prevents us from selling guns plugins.&#x20;

You can get your licenses transferred over for free by posting a thread in our discord asking for help transferring your license. Make sure to include the following information:

* Your spigot account (e.g. [https://www.spigotmc.org/members/cjcrafter1.447051/](https://www.spigotmc.org/members/cjcrafter1.447051/))
* Your pluginify account (e.g. [https://pluginify.org/members/cjcrafter.1/](https://pluginify.org/members/cjcrafter.1/))
* Which plugins you have purchased
* Proof of purchase

Discord is the only place to get support for this.
