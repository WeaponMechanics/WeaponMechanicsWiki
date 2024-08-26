---
description: Configurable weapon controls
---

# Trigger

```yaml
  Trigger:
    Main_Hand: <TriggerType>
    Off_Hand: <TriggerType>
    Dual_Wield:
      Main_Hand: <TriggerType>
      Off_Hand: <TriggerType>
    Circumstance:
      Reloading: <DENY/REQUIRED>
      Zooming: <DENY/REQUIRED>
      Sneaking: <DENY/REQUIRED>
      Standing: <DENY/REQUIRED>
      Walking: <DENY/REQUIRED>
      Riding: <DENY/REQUIRED>
      Sprinting: <DENY/REQUIRED>
      Dual_Wielding: <DENY/REQUIRED>
      Swimming: <DENY/REQUIRED>
      In_Midair: <DENY/REQUIRED>
      Gliding: <DENY/REQUIRED>
      Ammo_Empty: <DENY/REQUIRED>
      Deny_Mechanics: <Mechanics>
```

For `TriggerType`, you have the following options:

* `start_sneak`
* `end_sneak`
* `double_sneak`
* `start_sprint`
* `end_sprint`
* `right_click`
* `left_click`
* `drop_item`
* `jump`
* `double_jump`
* `start_swim`
* `end_swim`
* `start_glide`
* `end_glide`
* `swap_hands`
* `start_walk`
* `end_walk`
* `start_in_midair`
* `end_in_midair`
* `start_stand`
* `end_stand`

#### Main\_Hand

The trigger used when the weapon is held in the main hand.

#### Off\_Hand

The trigger used when the weapon is held in the off hand.&#x20;

#### Dual\_Wield

When dual-wielding weapons, you may want to change the trigger. For example, you may want to change the scoping trigger from `left_click` to `start_sneak`.&#x20;

* `Main_Hand` -> Dual wielding trigger for main hand.
* `Off_Hand` -> Dual wielding trigger for off hand.

#### Circumstance

Allows you to deny or force certain actions for the trigger to work. For example, you can deny shooting while sprinting or scoping while dual-wielding.&#x20;

For the following options, use:

1. `DENY` to prevent the trigger from working with this condition.
2. `REQUIRED` to force the entity to use this condition before the trigger works.
3. Delete the config line to allow the action.&#x20;

* `Reloading` -> If the shooter is reloading the weapon.
* `Zooming` -> If the shooter is currently scoping.
* `Sneaking` -> If the shooter is holding shift.&#x20;
* `Standing` -> If the shooter is not moving.
* `Walking` -> If the shooter is walking.
* `Riding` -> If the shooter is riding a mount.
* `Sprinting` -> If the shooter is sprinting.
* `Dual_Wielding` -> If the shooter is using 2 weapons.
* `Swimming` -> If the shooter is currently submerged underwater or sprint swimming.&#x20;
* `In_Midair` -> If the shooter is not on the ground.
* `Gliding` -> If the shooter is gliding with an elytra.
* `Ammo_Empty` -> If the held weapons are empty

#### Deny\_Mechanics

The mechanics to play when the trigger is denied. Usually, this is a sound queue (like an angry villager) or an action bar alerting the user that they cannot perform that action. Use the [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") wiki.

* `@Source{}` -> The player who attempted to use the trigger
* `<deny_reason>` -> Which "action" caused the denial.&#x20;
  * This will be 1 option from [#circumstance](trigger.md#circumstance "mention"), but lowercase.
  * For example, `Dual_Wielding` -> `dual wielding`.&#x20;

## Example

```yaml
  Scope:
    Trigger:
      Main_Hand: "LEFT_CLICK"
      Off_Hand: "LEFT_CLICK"
      Circumstance:
        Dual_Wielding: "DENY"
        Deny_Mechanics:
          - "ActionBar{message=<red><i>You cannot scope while <deny_reason>!}"
```

This example is taken from the `50_GS`, and will let players scope with the pistol by punching. If they are holding 2 weapons, players will not be able to scope.&#x20;
