---
description: Article explaining causes of lag in explosions, and how to reduce it!
---

# Optimizing Explosions

This article is for the [explosion](../weapon-modules/explosion/ "mention") feature of WeaponMechanics.

WeaponMechanics uses a custom explosion system; it is completely separate from the Minecraft code (_even though it looks very similar!_). WeaponMechanics, by default, uses a highly optimized Explosion algorithm. But what if you are still encountering lag?

## Falling Blocks

Falling blocks are visual effects added by [#block\_damage](../weapon-modules/explosion/#block\_damage "mention"). Although they are only visual, the math for calculating their collisions can cause a lot of lag. If you have a large explosion, you should either lower the chances for falling blocks, or completely disable them.

```yaml
<weapon>:
  Explosion:
    Block_Damage:
      Falling_Block_Chance: 5%  # Set this to 0% for best performance
```

## Reducing Rays

Explosions from WeaponMechanics are calculated the same way explosions from vanilla Minecraft are calculated; by casting $$16\cdot 16\cdot 6=1536$$ rays in all directions. _This is expensive on the CPU_, especially if you explosion yield is high ($$>10$$) or you have lots of explosions at the same time (Like an Airstrike).&#x20;

```yaml
<weapon>:
  Explosion:
    Explosion_Type_Data:
      Rays: 16  # 16 is the default value. Change to something like 12 for better performance
```

{% hint style="warning" %}
This trick only works for `Explosion_Shape: DEFAULT`, other explosion shapes will not work.
{% endhint %}

## Changing Explosion Shape

Using `Explosion_Shape: DEFAULT` will _always_ be taxing on the CPU. If you have a server that has 100s of explosions a minute, you should consider switching to a new shape, like `SPHERE`.&#x20;

See [#explosion\_shape](../weapon-modules/explosion/#explosion\_shape "mention") for more information.

## Changing Explosion Exposure

Using `Explosion_Exposure: DEFAULT` casts a lot of rays for each entity in the radius of the explosion. Switching to the optimized exposure can help reduce the number of rays.&#x20;

```yaml
<weapon>:
  Explosion:
    Explosion_Exposure: OPTIMIZED
```

For a more draconian route, you can use `DISTANCE` to perform almost NO math per entity (At the cost of drastically reducing the features of an explosion).
