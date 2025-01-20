# Reload

{% hint style="info" %}
If you want your gun to have **infinite ammo** and to never reload, you can delete the `Reload` module completely from your gun.&#x20;
{% endhint %}

```yaml
  Reload:
    Trigger: <Trigger>
    Magazine_Size: <amount>
    Ammo_Per_Reload: <amount>
    Unload_Ammo_On_Reload: <true/false>
    Reload_Duration: <ticks>
    Shoot_Delay_After_Reload: <ticks>
    Start_Mechanics: <Mechanics>
    Finish_Mechanics: <Mechanics>
    Ammo:  # Scroll down for more information
```

#### Trigger

The [trigger.md](../../trigger.md "mention") to use to trigger reloading.

#### Magazine\_Size

The maximum amount of ammo that can be loaded into the gun.

#### Ammo\_Per\_Reload

Use this feature to load bullets individually (some real-life guns have built-in magazines, which you load into 1 by 1). Otherwise, it defaults to [#magazine\_size](./#magazine_size "mention").&#x20;

#### Unload\_Ammo\_On\_Reload

Defines if ammo is unloaded on reload. This means that all remaining ammo in the weapon is taken out from the weapon, and if `Ammo` is defined, they're given back to the player.

#### Reload\_Duration

The time, in ticks, that it takes to reload the magazine.&#x20;

#### Shoot\_Delay\_After\_Reload

The time, in ticks, after a reload before the gun can be shot.

#### Start\_Mechanics

The mechanics triggered when the weapon starts reloading. Use the [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") wiki.

* `@Source{}` -> The entity holding the weapon.

#### Finish\_Mechanics

The mechanics triggered when the weapon completes reloading. Use the [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") wiki.

* `@Source{}` -> The entity holding the weapon.

#### Ammo

Check out the [ammo.md](ammo.md "mention") wiki page.



