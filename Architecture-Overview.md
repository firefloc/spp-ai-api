# Architecture Overview

SPP-AI follows a layered architecture designed for future extensibility via addons.

## Three-Layer Vision

### spp-core (Fabric Mod — Proprietary)
The core mod runs standalone with just Fabric + Carpet Mod. It contains:
- **PersonaManager** — Singleton managing all active personas
- **ActionEngine** — Priority-based decision stack (5 levels)
- **PersonaEntity** — FakePlayer wrapper with async pathfinding
- **SppPathfinder** — A* pathfinding (async off-tick, 2 threads)
- **ModuleRegistry** — Loads and manages behavior modules
- **ControlSurfaceRouter** — Dispatches control tasks to appropriate surfaces
- **Maestro** — Zone-based orchestrator (active chunks around connected players)
- **5 Core Modules** — EnvironmentSensor, Inventory, Threat, Survival, Build

### spp-lib (API Bridge — Future Public Module)
A separate Gradle module containing only the types needed by addon developers:
- Interfaces: PersonaModule, AbstractModule, BattleCapabilityProvider
- Records: ModuleContext, WorldSnapshot, ActionDecision
- Enums: ActionPriority, TickResult
- Wrapper: PersonaInventory
- Zero external dependencies (no Minecraft, no Cobblemon)

### spp-addons (Fabric Mods with Custom Entrypoints)
Each addon is a standard Fabric mod that declares a custom entrypoint:
```json
{
  "entrypoints": {
    "spp-addon": ["com.example.MyAddon"]
  }
}
```
spp-core discovers addons at startup via `FabricLoader.getInstance().getEntrypointContainers("spp-addon", SppAddonEntrypoint.class)`.

## Key Design Decisions

1. **No URLClassLoader** — Addons are Fabric mods, not custom-loaded JARs. This avoids Loom namespace mapping issues.
2. **CobblemonAdapter isolated** — Core uses `BattleCapabilityProvider` interface; Cobblemon-specific code lives in addon.
3. **Tests behind config flag** — `/spp test` commands hidden in prod via `enableDevTests` in `spp-persona.json`.
4. **RCT code isolated** — `RctIntegrationManager` extracted from PersonaManager, future addon candidate.

## Dependency Graph

```
spp-core depends on: spp-lib, carpet, fabric-api
spp-addon-rct depends on: spp-lib, cobblemon, rctmod
spp-lib depends on: (nothing — pure API)
```
