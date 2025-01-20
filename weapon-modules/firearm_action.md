# Firearm\_Action

```yaml
  Firearm_Action:
    Type: <FirearmType>
    Firearm_Action_Frequency: <use every x amount of shots>
    Open:
      Time: <ticks>
      Mechanics: <Mechanics>
    Close:
      Time: <ticks>
      Mechanics: <Mechanics>
```

#### **Type**

Defines how weapon's firearm actions will behave. There are 4 different firearm types. These firearm actions can add a layer of depth, especially if you have custom sounds for the firearm actions.

{% tabs %}
{% tab title="SLIDE" %}
For most magazine-fed weapons, if a magazine is not empty, the magazine can simply be replaced without additional firearm actions.

* When Shooting:
  * Weapon Fires
* When Reloading
  * If empty
    * Weapon Opens (Pull the slide back, specifically for H\&K weapons, AUG and others)
    * Weapon Reloads (Take out the magazine, insert new magazine)
    * Weapon Closes (Slide returns, a bullet is chambered)
  * If not empty
    * Weapon Reloads (Take out the magazine, insert new magazine)
{% endtab %}

{% tab title="REVOLVER" %}
For revolvers, the cylinder has to be pulled out so ammo can be loaded.

* _When Shooting_:
  * Weapon Fires
* _When Reloading_:
  * Weapon Opens (The rotating section pops out).
  * The reload-timer starts (Bullets are loaded into each slot).
  * Weapon Closes (The rotating section pops back in).
{% endtab %}

{% tab title="PUMP" %}
For pump-action weapons, a pump has to be cocked back and forth to eject and load a shell.

* _When Shooting_:
  * Weapon Fires
  * Weapon Opens (Ejecting a shell)
  * Weapon Closes (Loading a shell)
* _When Reloading_:
  * If empty
    * Weapon Reloads
    * Weapon Opens (If not already open, ejecting a shell)
    * Weapon Closes (Loading a shell)
  * If not empty
    * Weapon Reloads
{% endtab %}

{% tab title="LEVER" %}
For lever/bolt action weapons, a lever must be pulled then pushed to eject and load a round. Different from `PUMP` because the weapon **MUST** be opened before reloading.

* _When Shooting_:
  * Weapon Fires
  * Weapon Opens (Ejecting a round)
  * Weapon Closes (Loading a round)
* _When Reloading_:
  * If empty
    * Weapon Opens (Ejecting a round, and unlocking the mag)
    * Weapon Reloads
    * Weapon Closes (Loading a round, and blocking the mag)
  * If not empty
    * Weapon Reloads
{% endtab %}
{% endtabs %}

{% hint style="info" %}
When using firearm actions with different fire types

* `SINGLE` -> After shot firearm actions are triggered
* `BURST` -> After the burst is finished, firearm actions are triggered
* `AUTO` -> After cancelling full-auto firearm actions are triggered
{% endhint %}

**`Firearm_Action_Frequency`: \<Integer>**

Defines how often firearm actions are used.

If the current ammo amount after shooting is divisible by `Firearm_Action_Frequency` then firearm actions are triggered. For example, when `Firearm_Action_Frequency: 2`, firearm actions will be triggered if the weapon is shot and ammo left in its magazine is 18. If ammo left were `9`, firearm actions wouldn't be triggered.

#### Open

* `Time`
  * The time, in ticks, it takes to open the weapon.
* `Mechanics`
  * Delayed sound plays will be cancelled if firearm actions are cancelled.
  * Use the [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") wiki.

#### Close

* `Time`
  * The time, in ticks, it takes to close the weapon.
* `Mechanics`
  * Delayed sound plays will be cancelled if firearm actions are cancelled
  * Use the [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") wiki.
