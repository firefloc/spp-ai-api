# API Surface

Types marked **API-SURFACE** in the codebase will form the public spp-lib module. These types are considered stable — their signatures will not change without a major version bump.

## Stable Types (v1)

### Interfaces
| Type | Package | Description |
|------|---------|-------------|
| [PersonaModule](../API-Reference/PersonaModule) | `persona.module` | Core module interface |
| [BattleCapabilityProvider](../API-Reference/BattleCapabilityProvider) | `api` | Battle readiness check |

### Abstract Classes
| Type | Package | Description |
|------|---------|-------------|
| [AbstractModule](../API-Reference/AbstractModule) | `persona.module` | Base class with defaults |

### Records
| Type | Package | Description |
|------|---------|-------------|
| [ModuleContext](../API-Reference/ModuleContext) | `persona.module` | Evaluation context |
| [WorldSnapshot](../API-Reference/WorldSnapshot) | `persona.module` | World state snapshot |
| [ActionDecision](../API-Reference/ActionDecision) | `persona` | Decision output |

### Enums
| Type | Package | Description |
|------|---------|-------------|
| [ActionPriority](../API-Reference/ActionPriority) | `persona.module` | 5-level priority stack |
| [TickResult](../API-Reference/TickResult) | `persona.module` | Tick execution status |

### Wrappers
| Type | Package | Description |
|------|---------|-------------|
| [PersonaInventory](../API-Reference/PersonaInventory) | `persona.module` | Read-only inventory |

## Internal Types (not stable)

These types are used internally by spp-core and should not be relied upon by addons:
- `PersonaManager`, `PersonaEntity`, `ActionEngine`
- `SppPathfinder`, `SppMovements`, `SppNavigationConfig`
- `ControlSurface`, `ControlSurfaceRouter`, `ControlTask`
- `AgentRuntime`, `AgentContext`, `AgentType`
- `Maestro`, `DirectiveRegistry`
- `RctIntegrationManager`, `RctArchetypeConfig`

## Versioning Policy

- **spp-lib** follows semantic versioning
- Patch: bug fixes, no API changes
- Minor: new types or fields added, backwards compatible
- Major: breaking changes to existing API
