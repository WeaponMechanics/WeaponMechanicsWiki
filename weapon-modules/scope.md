---
description: Zoom in with your weapon
---

# Scope

```yaml
  Scope:
    Trigger: <Trigger>
    Night_Vision: <true/false>
    Pumpkin_Overlay: <true/false> # This is a WMC (Paid) feature
    Zoom_Amount: <1-10>
    Mechanics: <Mechanics>
    Shoot_Delay_After_Scope: <ticks>
    Zoom_Off:
      Trigger: <Trigger>
      Mechanics: <Mechanics>
    Zoom_Stacking:
      Stacks: 
        - <1-10>
        - <1-10>
        - <etc.>
      Mechanics: <Mechanics>
```

#### Trigger

This is the trigger used to actually use scope. Use [#trigger](scope.md#trigger "mention").

#### Night\_Vision

Whether to give entity night vision effect during scoping. The night vision potion is given via packets.

#### Pumpkin\_Overlay

{% hint style="warning" %}
This is a [WeaponMechanicsCosmetics](https://www.spigotmc.org/resources/104539/) (Paid) feature!
{% endhint %}

When this is a true, a _"fake"_ pumpkin will be put on the player's head. This can be used to create a scope reticle. Check `WeaponMechanicsCosmetics > config.yml` to change the name/lore of the pumpkin. Note that this feature doesn't work for players in Creative mode! Since creative players can duplicate items, the pumpkin sometimes stays on the head even after leaving the scope. For survival players, this is only a visual effect. If they were previously wearing a helmet, the server (and every other player) still thinks the shooter is wearing a helmet.

<details>

<summary>Scope Reticle Image</summary>

<img src="https://user-images.githubusercontent.com/43940682/189747433-f1c82f3e-c757-47c7-9845-121146f15db8.png" alt="reticle" data-size="original">

</details>

#### Zoom\_Amount

Defines the zoom amount. The value has to be between `1` and `10`. Where `1` is lowest and `10` is the highest zoom. You can also use decimals like `2.6`, `4.8`, etc.

#### Mechanics

Mechanics triggered when the player scopes in. Use [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention").&#x20;

#### Shoot\_Delay\_After\_Scope

If this gun zooms in, this is the time in ticks (20 ticks = 1 second) after the entity is able to fire the gun.

#### Zoom\_Off

* `Trigger`
  * If you want unscoping to use a different trigger, you can define that here.
  * For most use cases, you can just delete this line.
  * Use [trigger.md](../trigger.md "mention").
* `Mechanics`
  * These mechanics are run when entity zooms out.
  * Use [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention").

{% hint style="info" %}
If you use `start_sneak`, then you should use `end_sneak` here for the trigger. Otherwise, the plugin will force players to sneak (press shift) twice to scope and to unscope.&#x20;
{% endhint %}

#### Zoom\_Stacking

Zoom stacking allows you to create multiple "levels" to zoom to. After the stacking reaches a maximum value, it will zoom out. Using the `Zoom_Off.Trigger`, you can exit zoom stacking prematurely.

* `Stacks`
  * Defines the list of zoom stacks
  * After initial `Zoom_Amount` this list is used in given order
* `Mechanics`
  * These mechanics are run when entity stacks zoom.
  * Use [#mechanics](scope.md#mechanics "mention").&#x20;

In this example there is 2 stacks, and `1.5` is the first zoom amount. Basically the order here is `1.5` -> `3.0` -> `7.0` -> zoom out

```yml
  Scope:
    Trigger:
      Main_Hand: "LEFT_CLICK"
      Off_Hand: "LEFT_CLICK"
    Zoom_Amount: 1.5
    Zoom_Stacking:
      Stacks:
        - 3.0
        - 7.0
```
