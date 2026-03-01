# SPP-AI — Scentient Player Persona

SPP-AI is a Fabric mod for Minecraft 1.21.1 that creates autonomous AI-driven player personas and NPC behaviors. Personas are full player entities (via Carpet Mod's FakePlayer) that navigate, survive, and interact with the world using a modular behavior system.

## Key Concepts

- **Persona**: An AI-controlled player entity that persists when its owner disconnects
- **ActionEngine**: Priority-based decision stack (SAFETY > EXPLICIT > MAINTENANCE > OBSERVED > STANDBY)
- **PersonaModule**: Pluggable behavior modules that make decisions at specific priority levels
- **ControlSurface**: Abstraction layer for controlling different entity types (FakePlayers, RCT trainers)

## Quick Links

- [Architecture Overview](Architecture-Overview) — spp-core / spp-lib / spp-addons vision
- [Getting Started](Getting-Started) — Dev environment setup
- [API Reference](API-Reference/PersonaModule) — Full module API documentation
- [Creating a Module](Modules/Creating-A-Module) — Step-by-step guide
- [Command Reference](Commands/Command-Reference) — All `/spp` commands

## Current Version

- **Minecraft**: 1.21.1
- **Fabric Loader**: 0.18.4
- **Dependencies**: Carpet Mod (required), Cobblemon + RCT Mod (optional)
- **Module API**: v1 (5 core modules: M01-M05)

## Project Structure

```
spp-core (Fabric mod — proprietary)
  ├── PersonaManager, ActionEngine, PersonaEntity
  ├── Modules M01-M05 (EnvironmentSensor, Inventory, Threat, Survival, Build)
  ├── SppPathfinder (A* async off-tick)
  └── ControlSurface router

spp-lib (API bridge — future public module)
  ├── PersonaModule, AbstractModule interfaces
  ├── ModuleContext, WorldSnapshot, PersonaInventory
  ├── ActionDecision, ActionPriority, TickResult
  └── BattleCapabilityProvider

spp-addons (Fabric mods using custom entrypoints — future)
  └── spp-addon-rct (Cobblemon + RCT integration)
```
