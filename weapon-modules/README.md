---
description: All configuration sections you can add to your weapons
---

# Weapon Modules

{% hint style="info" %}
New to the wiki? This page contains **important information** about config! Read this first!
{% endhint %}

## Weapon Title

All weapons have a unique "weapon title" in config. It is the name at the top of the file, like:

<figure><img src="../.gitbook/assets/image (1).png" alt="the weapon title is the root key in the yaml file" width="375"><figcaption></figcaption></figure>

In the image above, the weapon title is `AK_47`. To get the weapon in your server, use `/wm get AK_47`.

{% hint style="danger" %}
The names of files are completely ignored. We suggest matching them with your weapon title (e.g., `AK_47.yml`), but this is optional and does not affect the plugin.
{% endhint %}

{% hint style="danger" %}
Your weapon title (And ALL OTHER config options) should **never** use any character other then a->z, A->Z, 0->9, and underscores `_`. Do NOT use periods or dashes.&#x20;
{% endhint %}

## Modules

All weapons use modules. A "Module" is a fancy way of saying a section in your config. For example, the [shoot](shoot/ "mention") module is required for all weapons. It goes under your weapon name in the config with 2 spaces. Let's look at an example of the `AK_47`:

```yaml
AK_47:
  Shoot:
    # Other options go here, like Trigger and Projectile_Speed
```

Most modules can also have sections inside. For example:

```yaml
AK_47:
  Shoot:
    Trigger: 
      # Other options go here, like Main_Hand and Off_Hand
```

Here is the complete list of modules (You can also see this on the sidebar on the left of this page!):

1. [info.md](info.md "mention")
2. [shoot](shoot/ "mention")
   1. [spread.md](shoot/spread.md "mention")
   2. [recoil.md](shoot/recoil.md "mention")
   3. [Broken link](broken-reference "mention")
3. [scope.md](scope.md "mention")
4. [reload](reload/ "mention")
   1. [ammo.md](reload/ammo.md "mention")
5. [skin.md](skin.md "mention")
6. [projectile](projectile/ "mention")
7. [explosion](explosion/ "mention")
8. [damage](damage/ "mention")
9. [firearm\_action.md](firearm_action.md "mention")
10. [melee.md](melee.md "mention")
11. [Firemode](https://app.gitbook.com/s/9hOjsLnIiB5Xm8MOXgWU/firemode "mention") <mark style="color:yellow;">-> Requires WeaponMechanicsPlus</mark>
12. [Cosmetics](https://app.gitbook.com/s/k51Oxya0kO19Qw62TtkL/cosmetics "mention") <mark style="color:yellow;">-> Requires WeaponMechanicsCosmetics</mark>
13. [Trails](https://app.gitbook.com/s/k51Oxya0kO19Qw62TtkL/trails "mention") <mark style="color:yellow;">-> Requires WeaponMechanicsCosmetics</mark>
14. [Show Time](https://app.gitbook.com/s/k51Oxya0kO19Qw62TtkL/show-time "mention") <mark style="color:yellow;">-> Requires WeaponMechanicsCosmetics</mark>

## Required Modules

The [info.md](info.md "mention") and [shoot](shoot/ "mention") modules are the only required modules. _Most_ config options are optional and can be omitted from your config file.&#x20;
