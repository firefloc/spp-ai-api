# ActionDecision

`org.scentient.spp.persona.ActionDecision`

Immutable decision record produced by modules and ActionEngine. The engine picks the highest-priority non-empty decision each evaluation cycle.

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `type` | `ActionType` | The kind of action to perform |
| `target` | `Vec3d` | Target position (nullable for IDLE, EAT) |
| `label` | `String` | Human-readable label for logging |

## ActionType Enum

| Value | Description |
|-------|-------------|
| `FLEE` | Emergency: flee from danger (lava, void, fire) |
| `MOVE_TO` | Navigate to a specific position |
| `IDLE` | Stop and hold position |
| `SEEK_HEAL` | Navigate to a healing station (Pokecenter) |
| `FOLLOW` | Follow a target entity position |
| `EAT` | Eat food from inventory |

## Factory Methods

```java
ActionDecision.flee(Vec3d safePos)
ActionDecision.moveTo(Vec3d pos, String label)
ActionDecision.idle(String label)
ActionDecision.seekHeal()
ActionDecision.seekHeal(Vec3d pokecenterPos)
ActionDecision.follow(Vec3d targetPos)
ActionDecision.eat(String label)
```

## Stability

Marked **API-SURFACE** — part of the public spp-lib API. New ActionType values may be added in future versions.
