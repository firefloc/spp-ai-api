# Addon System Overview

> **Status**: Architecture designed, implementation planned for Brique 7.

## Vision

SPP addons are standard Fabric mods that extend spp-core via a stable API bridge (spp-lib). Each addon registers behavior modules, control surfaces, or capabilities that integrate seamlessly with the core Persona system.

## How It Works

1. Addon declares a custom Fabric entrypoint in its `fabric.mod.json`:
   ```json
   {
     "entrypoints": {
       "spp-addon": ["com.example.MyAddon"]
     }
   }
   ```

2. Addon implements `SppAddonEntrypoint`:
   ```java
   public class MyAddon implements SppAddonEntrypoint {
       @Override
       public void onLoad(ModuleRegistry registry) {
           registry.register(new MyCustomModule());
       }
   }
   ```

3. spp-core discovers addons at startup:
   ```java
   FabricLoader.getInstance()
       .getEntrypointContainers("spp-addon", SppAddonEntrypoint.class)
       .forEach(c -> c.getEntrypoint().onLoad(registry));
   ```

## Why Fabric Entrypoints?

- **No URLClassLoader** — avoids Loom namespace mapping issues
- **Standard Fabric tooling** — addons build, remap, and distribute like any Fabric mod
- **Dependency management** — `fabric.mod.json` declares `depends: { "scentient_spp": ">=1.0.0" }`
- **Crash isolation** — a broken addon is a broken mod, identified by Fabric's standard crash reports

## Planned Addons

- **spp-addon-rct**: Cobblemon + RCT trainer integration (first addon, Brique 7)
