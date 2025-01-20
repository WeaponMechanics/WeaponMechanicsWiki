# Block Damage

Block Damage is used for [.](./ "mention") and in WeaponMechanicsCosmetics.

{% embed url="https://youtu.be/C5aRJAhPECI" %}
Advanced Block Damage tutorial
{% endembed %}

```yaml
    Block_Damage:
      Drop_Broken_Block_Chance: <Chance>
      Damage_Per_Hit: <Integer>
      Default_Block_Durability: <Integer>
      Default_Mode: <CANCEL/BREAK/CRACK>
      Default_Mask: <Material>
      Blocks:
        - <Material*> <CANCEL/BREAK/CRACK*> <ShotsToBreakBlock> <Mask>
```

#### Drop\_Broken\_Block\_Change

The chance to drop the broken block as an item for players to pick up. Defaults to `0%`.&#x20;

{% hint style="danger" %}
Using `Drop_Broken_Block_Chance` with [#regeneration](./#regeneration "mention") will cause duplication.
{% endhint %}

#### Damage\_Per\_Hit

The amount of damage points to deal to the block. Defaults to `1`.

#### Default\_Block\_Durability

Defines how many hits it takes to break blocks. This can be overridden per block in [#blocks](block-damage.md#blocks "mention").

#### Default\_Mode

Defines how the block should show damage:

* `CANCEL` -> Don't apply any damage to the block.
* `CRACK` -> Show block crack animation, but do not break the blocks.
* `BREAK` -> Show block crack animation, and break block when fully damaged.&#x20;

This can be overridden per block in [#blocks](block-damage.md#blocks "mention").

#### Default\_Mask

Defines the [Material](https://app.gitbook.com/s/IIUkVnlH40vVBzLhWWQ8/references#material "mention") used to replace the block. Defaults to `AIR`.

This can be overridden per block in [#blocks](block-damage.md#blocks "mention").

{% hint style="info" %}
If you want to replace blocks with data (for example, stairs), go into:

> <mark style="color:yellow;">**server -> plugins -> WeaponMechanics -> config.yml**</mark>

And set:

```yaml
Explosions:
  Attempt_Copy_Data: true  # set this to true
```
{% endhint %}

#### Blocks

Defines the list of block overrides.

Format is:

> **\<block to break> \<CANCEL/CRACK/BREAK> \<shots to break> \<mask>**

Examples:

* `BEDROCK CANCEL` -> Prevents bedrock from being broken.
* `DIRT BREAK` -> Destroys dirt in 1 shot.
* `OBSIDIAN CRACK 5` -> Shows the crack animation for obsidian, but doesn't break.&#x20;
* `GRAY_STAINED_GLASS BREAK 1 DIRT` -> Destroys gray glass in 1 shot and replaces it with dirt.
* `$glass BREAK 2` breaks all glass block types in 2 shots.&#x20;

## Example

This is a standard example that the average server should use. This example will break all blocks (except for non-breakable blocks):

```yaml
    Block_Damage:
      Spawn_Falling_Block_Chance: 0.55  # Used for Explosions
      Default_Mode: BREAK
      Blocks:
        - "BEDROCK cancel"
        - "$WATER cancel"  # stationary_water and moving_water for 1.12 support
        - "OBSIDIAN cancel"
        - "$LAVA cancel"  # stationary_lava and moving_lava for 1.12 support
```

