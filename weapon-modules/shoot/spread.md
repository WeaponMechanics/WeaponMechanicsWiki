# Spread

Spread lets you control the randomness in the direction after shooting. In general, you don't want bullets to fly perfectly straight, you want some random angle. Video Games all handle this differently, but in general, you should make your first shot fairly accurate, and increase spread over time.

{% hint style="info" %}
Spread $$\ne$$ Accuracy. Spread is the **opposite** of accuracy. Lower spreads mean higher accuracy.&#x20;
{% endhint %}

```yaml
    Spread:
      Spread_Image:
        Name: <path>
        Field_Of_View_Width: <degrees> 
        Field_Of_View_Height: <degrees> 
      Base_Spread: <base spread>
      Modify_Spread_When:
        Zooming: <amount> or <amount>%
        Sneaking: <amount> or <amount>%
        Standing: <amount> or <amount>%
        Walking: <amount> or <amount>%
        Riding: <amount> or <amount>%
        Sprinting: <amount> or <amount>%
        Dual_Wielding: <amount> or <amount>%
        Swimming: <amount> or <amount>%
        In_Midair: <amount> or <amount>%
        Gliding: <amount> or <amount>%
      Changing_Spread:
        Starting_Amount: <amount>
        Reset_Time: <ticks>
        Increase_Change_When:
          Always: <amount> or <amount>%
          Zooming: <amount> or <amount>%
          Sneaking: <amount> or <amount>%
          Standing: <amount> or <amount>%
          Walking: <amount> or <amount>%
          Riding: <amount> or <amount>%
          Sprinting: <amount> or <amount>%
          Dual_Wielding: <amount> or <amount>%
          Swimming: <amount> or <amount>%
          In_Midair: <amount> or <amount>%
          Gliding: <amount> or <amount>%
        Bounds:
          Reset_After_Reaching_Bound: <true/false>
          Minimum: <minimum spread>
          Maximum: <maximum spread>
```

#### Spread\_Image

Spread images are `.png` files in the <mark style="color:yellow;">**your server -> plugins -> WeaponMechanics -> spread\_patterns**</mark> folder. You can use this feature along with other spread features to accurately replicate spread from video games.

* `Name`
  * The name of the image file (For example, `"circle.png"`).&#x20;
* `Field_Of_View_Width`
  * The "maximum angle" of the image.&#x20;
  * If you set this to `45.0`, then the pixels on the edge of the image will be at a 45 degree angle.&#x20;
  * Defaults to `45.0`.
* `Field_Of_View_Height`
  * Same as `Field_Of_View_Width`, but for the vertical angle instead.

{% hint style="info" %}
If you create your image files, make sure to only use grayscale colors! It is recommended to keep image files smaller than 128x128, but there is no CPU impact on differently-sized images.
{% endhint %}

#### Base\_Spread

The randomness applied to all shots. Applied both vertically, and horizontally.&#x20;

#### Modify\_Spread\_When

Modifies the amount of spread based on what the player is doing. For example, when the player is scoping, you probably want to _reduce_ spread.

* `Zooming` -> when scoping with the weapon
* `Sneaking` -> When the player is holding shift
* `Standing` -> When the shooter is not moving
* `Walking` -> When the shooter is moving
* `Riding` -> When the shooter is riding an entity
* `Sprinting` -> When the player is sprinting
* `Dual_Wielding` -> When the shooter has weapons in both hands
* `Swimming` -> When the shooter is in water
* `In_Midair` -> When the shooter is in the air
* `Gliding` -> When the shooter is gliding using an elytra

For example:

```yaml
      Modify_Spread_When:
        Zooming: -5  # Increase accuracy when scoped
        Sneaking: -2
        Walking: 1.5
        Riding: 3.0
        Sprinting: 2.5
        Swimming: 1.5
        In_Midair: 4
        Gliding: 5
```

#### Changing\_Spread

Changes the spread after every consecutive shot. This can be used to make guns inaccurate if you spam.&#x20;

* `Starting_Amount`
  * The base change amount.
  * If you want the first shot to be accurate, use `0`.&#x20;
* `Reset_Time`
  * The time, in ticks, it takes to reset spread back to `Starting_Amount`.
  * The timer resets after every shot.
* `Increase_Change_When`
  * This works just like [#modify\_spread\_when](spread.md#modify\_spread\_when "mention")
  * `Always` -> Every shot
  * \+ all options from [#modify\_spread\_when](spread.md#modify\_spread\_when "mention")
* `Bounds`
  * Defines the minimum and maximum spreads.
  * `Reset_After_Reach_Bounds`
    * Use `true` to reset back to `Starting_Amount`
    * Use `false` so the spread stays high for people spamming the gun.
  * `Minimum`
    * The lowest spread value allowed.
  * `Maximum`
    * The highest spread value allowed.
