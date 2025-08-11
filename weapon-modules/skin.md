---
description: Changes weapon item to different skins/positions
---

# Skin

You may have noticed that when you are holding one of the default weapons, and you left-click to aim, the weapon changes positions. Or when you start sprinting, the gun changes places to point downward as if you were holding it with 2 hands. This is the `Skin:` module in action.

{% hint style="danger" %}
## Legacy

Are you using 1.12.2 or 1.13.2? Minecraft versions older than 1.14.4 cannot use Custom\_Model\_Data and must use the legacy system. You may still use the legacy system on newer versions if you think it is easier to use:

<details>

<summary>Legacy System</summary>

The legacy skin system works with **hard set** values instead of adding numbers together. Here are all the options available:

<pre class="language-yaml"><code class="lang-yaml">  Skin:
    Default:
      Type: &#x3C;Material>
      Legacy_Data: &#x3C;Integer>
      Custom_Model_Data: &#x3C;Integer>
      Item_Model: "namespace:key"
      Durability: &#x3C;Integer>
    Scope:
      Type: &#x3C;Material>
      Legacy_Data: &#x3C;Integer>
      Custom_Model_Data: &#x3C;Integer>
      Item_Model: "namespace:key"
      Durability: &#x3C;Integer>
<strong>    Scope_&#x3C;number>:
</strong>      Type: &#x3C;Material>
      Legacy_Data: &#x3C;Integer>
      Custom_Model_Data: &#x3C;Integer>
      Item_Model: "namespace:key"
      Durability: &#x3C;Integer>
    No_Ammo:
      Type: &#x3C;Material>
      Legacy_Data: &#x3C;Integer>
      Custom_Model_Data: &#x3C;Integer>
      Item_Model: "namespace:key"
      Durability: &#x3C;Integer>
    Reload:
      Type: &#x3C;Material>
      Legacy_Data: &#x3C;Integer>
      Custom_Model_Data: &#x3C;Integer>
      Item_Model: "namespace:key"
      Durability: &#x3C;Integer>
    Sprint:
      Type: &#x3C;Material>
      Legacy_Data: &#x3C;Integer>
      Custom_Model_Data: &#x3C;Integer>
      Item_Model: "namespace:key"
      Durability: &#x3C;Integer>
</code></pre>



* `Type`:
  * The material of the skin, if the material changed.
  * For **most** usages, you can delete this line. I personally recommend keeping your weapon skins to 1 item type.
* `Legacy_Data`:
  * The material data used in minecraft versions 1.8.8 through 1.12.2.
  * Usually used for wool colors.
* `Custom_Model_Data`:
  * A number where your model is defined.
  * For help creating a resource pack using model data, see [CustomModelData](https://www.planetminecraft.com/forums/communities/texturing/new-1-14-custom-item-models-tuto-578834/).
  * This can only be used in minecraft versions 1.14 and higher.
* `Item_Model`:
  * The custom model location in your resource pack, formatted as "`namespace:key"`
* `Durability`:
  * A number where your model is defined.
  * For help creating a resource pack using durability, see [Durability](https://www.spigotmc.org/wiki/custom-item-models-in-1-9-and-up/).
  * If your server uses versions 1.14 or higher, I highly recommend using `Custom_Model_Data` instead.
  * This can only be used in minecraft versions 1.9 and higher.

Here is an example config:

```yaml
  Skin:
    Default: 
      Custom_Model_Data: 5
    Scope: 
      Custom_Model_Data: 1005
    Sprint:
      Custom_Model_Data: 2005
```

You can see that the "hip fire" or default skin will use a custom model data of 5, and when you scope, the custom model data will be set tot 1005.&#x20;

</details>
{% endhint %}

```yaml
  Skin:
    Default: <integer>
    Scope: ADD <integer>
    Scope_<number>: ADD <integer>
    No_Ammo: ADD <integer>
    Reload: ADD <integer>
    Sprint: ADD <integer>
   
    # This requires WeaponMechanicsCosmetics to be installed
    <skin>: ADD <integer>
    <another skin>: ADD <integer>
    
    # This required WeaponMechanicsPlus to be installed
    Attachments:
      <attachment title>: ADD <integer>
      <another attachment>: ADD <integer>
```

Only 1 of `Default`, `Scope`, `Scope_<number>`, `No_Ammo`, `Reload`, and `Sprint` can be shown simultaneously. If you are Sprinting and Scoping simultaneously, the `Sprint` skin will be used since it has a higher priority. Here is the priority order:

> <mark style="color:yellow;">**No\_Ammo -> Scope\_\<number> -> Scope -> Reload -> Sprint -> Default**</mark>

1. The `Default` skin is the hip-fire skin.
2. The `Scope` skin is used for aiming down iron sights.
   1. You can also change the model for each stacked scope level
   2. For example, use `Scope_1` to replace the first stacked zoom (Remember that the first stacked zoom is the second zoom)
   3. You can use this to create [canted sights](https://support.pubg.com/hc/en-us/articles/360016470833-What-is-a-Canted-Sight-)
3. The `Reload` skin is used while loading ammo into the weapon.&#x20;
4. The `Sprint` skin is used while the player is sprinting.
5. The `No_Ammo` skin is used when the gun has no loaded ammo.

## Add

See how all options (except `Default`) require the "ADD \<integer>" option? Instead of setting the skin to a number, we sum up all the options. This allows us to keep configs relatively small, as long as we keep our resource packs organized. If you are having trouble, check out the tutorial below:

{% embed url="https://youtu.be/6FVtGOQwQLE" %}
in-depth skin tutorial video
{% endembed %}

## Skins

{% hint style="warning" %}
[WeaponMechanicsCosmetics](https://www.spigotmc.org/resources/weaponmechanicscosmetics-guns-in-minecraft-1-12-2-1-20-1.104539/) must be purchased and installed to use skins
{% endhint %}

Want to get donations from players? Skins are perfect for getting players to support your development! Check out this example from the `AK_47`:

```yaml
  Skin:
    Default: 5
    Scope: ADD 1000
    Sprint: ADD 2000
    blue: ADD 10000 # blue and red will only work if you have purchased WMC
    red: ADD 20000
```

When holding the `AK_47`, you can use `/skin blue` or `/skin red` to change the weapon's skin (As long as you have the `weaponmechanics.skin.AK_47.blue` and `weaponmechanics.skin.AK_47.red` permissions).

{% hint style="success" %}
The `weaponmechanics.skin.*` permission gives players access to every skin for every gun. The `weaponmechanics.skin.AK_47.*` permission gives players access to every skin for the AK\_47.&#x20;
{% endhint %}

## Attachments

{% hint style="warning" %}
WeaponMechanicsPlus must be purchased and installed to use attachments
{% endhint %}

Let's say you want to add a reflex sight to your weapon. This means you want to change the skin, so instead of seeing iron sights when you scope, you want a "dot" sight. Let's say you have an attachment called `Reflex_Sight`. Here is what you can do:

```yaml
  Skin:
    # Define other options here, such as Default and Scope
    Attachments:
      Reflex_Sight: ADD 100000
```
