---
description: How to clone the WeaponMechanics repo
---

# Cloning Repository

{% embed url="https://youtu.be/2hT9ZuDQ5MA" %}
YouTube tutorial
{% endembed %}

Since WeaponMechanics uses `net.minecraft.server` code, we have to have a compiled server jar for every latest Minecraft version (1.12+). After cloning the GitHub repository, navigate to:

> <mark style="color:yellow;">**MechanicsMain -> lib -> download-spigot-lib.bat**</mark>

Running that batch file will download the latest [BuildTools](https://www.spigotmc.org/wiki/buildtools/) from Spigot and run it for each Minecraft version (<1.17). For Minecraft versions 1.17 and higher, we use [paperweight](https://github.com/PaperMC/paperweight-test-plugin), a Gradle plugin that automatically downloads the server jar. You only need to run this file once.&#x20;

Afterward, I suggest running `remove-craftbukkit-jars.bat` and `clean-buildtools.bat` to delete all unnecessary downloads.&#x20;

