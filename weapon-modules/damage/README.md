# Damage

```yaml
  Damage:
    Base_Damage: <amount>
    Base_Explosion_Damage: <amount>
    Fire_Ticks: <ticks>
    Enable_Owner_Immunity: <true/false>
    Ignore_Teams: <true/false>
    Armor_Damage: <Integer>
    Mechanics: <Mechanics>
    Head:
      Bonus_Damage: <amount>
      Mechanics: <Mechanics>
    Body:
      Bonus_Damage: <amount>
      Mechanics: <Mechanics>
    Arms:
      Bonus_Damage: <amount>
      Mechanics: <Mechanics>
    Legs:
      Bonus_Damage: <amount>
      Mechanics: <Mechanics>
    Feet:
      Bonus_Damage: <amount>
      Mechanics: <Mechanics>
    Backstab:
      Bonus_Damage: <amount>
      Mechanics: <Mechanics>
    Critical_Hit:
      Chance: <1-100>
      Bonus_Damage: <amount>
      Mechanics: <Mechanics>
    Kill:
      Mechanics: <Mechanics>
    Damage_Modifiers: <DamageModifiers> # see below for more information
    Explosion:
      Damage_Modifiers: <DamageModifiers> # see below for more information
    Dropoff:
    - <travel distance> <damage amount>
```

Damage is calculated by summing base damage, and then applying all [#damage-modifiers](./#damage-modifiers "mention").&#x20;

#### Base\_Damage

The amount of damage before any damage modifiers are applied.&#x20;

#### Base\_Explosion\_Damage

The amount of damage the [explosion](../explosion/ "mention") deals (at the center of the explosion).&#x20;

#### Fire\_Ticks

Lights the damaged entity on fire for a set amount of time (time in ticks). For example, `Fire_Ticks: 100` will light the entity on fire for 5 seconds if a projectile from this weapon OR the explosion hits it).&#x20;

#### Enable\_Owner\_Immunity&#x20;

Use `true` to prevent the shooter from taking damage from their shots. This makes the shooter immune to their own [explosion](../explosion/ "mention").&#x20;

#### Ignore\_Teams

By default, guns will respect teams that prevent damage (Teams are added by Minecraft using the `/team` command). Use `Ignore_Teams: true` to enable friendly fire.&#x20;

#### Armor\_Damage

Defines how much damage to apply to the victim's armor. You probably want this number to be small, like `1` or `2`.

#### Mechanics

The mechanics to trigger when damaging an entity. Use the [Mechanics](https://app.gitbook.com/o/MgHAZkcfIhs3YcmBjk2r/s/hz7yMxlL81NxAT44nraH/ "mention") wiki.&#x20;

* `@Source{}` -> The shooter.
* `@Target{}` -> The entity being damaged (the victim).

#### Head

* `Bonus_Damage` -> Defines how much additional damage head shots deal.
* `Mechanics` -> Mechanics to trigger after a head shot.
  * `@Source{}` -> The shooter.
  * `@Target{}` -> The entity who was shot in the head.

#### Body

* `Bonus_Damage` -> Defines how much additional damage body shots deal.
* `Mechanics` -> Mechanics to trigger after a body shot.
  * `@Source{}` -> The shooter.
  * `@Target{}` -> The entity who was shot in the chest.

#### Legs

* `Bonus_Damage` -> Defines how much additional damage leg shots deal.
* `Mechanics` -> Mechanics to trigger after a leg shot.
  * `@Source{}` -> The shooter.
  * `@Target{}` -> The entity who was shot in the legs.

#### Feet

* `Bonus_Damage` -> Defines how much additional damage a foot shot deals.
* `Mechanics` -> Mechanics to trigger after a foot shot.
  * `@Source{}` -> The shooter.
  * `@Target{}` -> The entity who was shot in the foot.

#### Backstab

Backstabs happen whenever the damage source comes from behind (In the $$180^{\circ}$$ area behind the victim).&#x20;

* `Bonus_Damage` -> Defines how much additional damage a foot shot deals.
* `Mechanics` -> Mechanics to trigger after a foot shot.
  * `@Source{}` -> The shooter.
  * `@Target{}` -> The entity who was backstabbed.

#### Critical\_Hit

* `Chance` -> Chance for a critical hit. Use `100` for 100% chance.&#x20;
* `Bonus_Damage` -> Defines how much additional damage a foot shot deals.
* `Mechanics` -> Mechanics to trigger after a foot shot.
  * `@Source{}` -> The shooter.
  * `@Target{}` -> The entity who was critically hit.

#### Kill

* `Mechanics` -> Mechanics to trigger after a foot shot.
  * `@Source{}` -> The shooter.
  * `@Target{}` -> The entity who was shot in the foot.

#### Damage\_Modifiers

The [#damage\_modifiers](./#damage\_modifiers "mention") to override the base damage modifiers (Defined in the `config.yml`).&#x20;

#### Explosion.Damage\_Modifiers

The [#damage\_modifiers](./#damage\_modifiers "mention") to override the base damage modifiers but for explosions (Defined in the `config.yml`).

#### Dropoff

Defines how much projectile travel distance will increase or decrease damage.

* `travel distance`
  * How far must the projectile go before this dropoff activates?
  * If the projectile has traveled `9` blocks and this list only has `10 -3`, then damage won't be decreased by `3` since that `10` blocks wasn't reached.
  * See [#100](https://github.com/WeaponMechanics/MechanicsMain/issues/100) if you want a "smooth" dropoff instead.
* `damage amount`
  * The amount to increase (`+`) or decrease (`-`) damage.
  * This number should probably _always_ be negative since you want projectiles to deal less damage
