# Projectile Scripts

A projectile "script" class can modify a projectile while in flight. This system is inspired by Unity's script system. Look at [ProjectileScript.java](https://github.com/WeaponMechanics/MechanicsMain/blob/master/WeaponMechanics/src/main/java/me/deecaad/weaponmechanics/weapon/projectile/ProjectileScript.java#L24) for a better idea.

To use scripts, you must do 2 things:

1. Create a `ProjectileScriptManager.`
2. Attach scripts to projectiles.

Let's take a closer look at how WeaponMechanicsCosmetics adds particles to falling blocks:

## Creating a Projectile Script

```java
public class FallingBlockScript extends ProjectileScript<AProjectile> {

    private Object data; // either BlockData (1.13+) or MaterialData (1.12-)

    public FallingBlockScript(@NotNull Plugin owner, @NotNull AProjectile projectile) {
        super(owner, projectile);

        if (projectile.getDisguise() == null || projectile.getDisguise().getType() != EntityType.FALLING_BLOCK)
            throw new IllegalArgumentException("Tried to attach to " + projectile + " when it doesn't have falling block");

        data = projectile.getDisguise().getData();
    }

    @Override
    public void onTickEnd() {
        Configuration config = WeaponMechanicsCosmetics.getInstance().getConfiguration();
        int amount = config.getInt("Explosion_Effects.Falling_Block_Dust.Amount");
        double spread = config.getDouble("Explosion_Effects.Falling_Block_Dust.Spread");

        if (amount != 0) {
            World world = projectile.getWorld();
            Location location = projectile.getLocation().toLocation(world);
            world.spawnParticle(Particle.FALLING_DUST, location, amount, spread, spread, spread, data);
        }
    }
}
```

This script will spawn a dust particle every tick on the projectile's location.&#x20;

## Projectile Script Manager

```java
public class CosmeticsScriptManager extends ProjectileScriptManager {

    public CosmeticsScriptManager(Plugin plugin) {
        super(plugin);
    }

    @Override
    public void attach(@NotNull AProjectile aProjectile) {
        if (aProjectile.getIntTag("explosion-falling-block") == 1) {
            FallingBlockScript script = new FallingBlockScript(getPlugin(), aProjectile);
            aProjectile.addProjectileScript(script);
            return;
        }
        
        // snip... other WMC stuff is below this, we use 1 manager to attach all scripts
    }
}
```

This manager will attach the falling block script to all projectiles marked with the `explosion-falling-block` tag.

## Registering the Script Manager

```java
WeaponMechanics.getProjectilesRunnable().addScriptManager(new CosmeticsScriptManager(plugin));
```

This code will inject your script manager, and begin listening for newly spawned projectiles! But wait, after someone runs `/wm reload`, your script will be gone! So instead of running this `onEnable()`, we should be running it after WeaponMechanics reloads config.&#x20;

So use the following listener:

```java
    @EventHandler
    public void queueSerializers(QueueSerializerEvent event) {
        if (!event.getSourceName().equals("WeaponMechanics"))
            return;
        
        WeaponMechanics.getProjectilesRunnable().addScriptManager(new CosmeticsScriptManager(plugin));  
    }
```
