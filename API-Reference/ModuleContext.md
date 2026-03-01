# ModuleContext

`org.scentient.spp.persona.module.ModuleContext`

Immutable context record passed to `PersonaModule.evaluate()` each cycle. Contains everything a module needs to make a decision. Built once per ActionEngine evaluation — shared across all modules.

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `personaUuid` | `UUID` | The persona's unique identifier |
| `environment` | [WorldSnapshot](WorldSnapshot) | Immutable snapshot of the world around the persona |
| `inventory` | [PersonaInventory](PersonaInventory) | Read-only view of the persona's inventory |
| `actionLog` | `ActionLog` | Historical action log for behavior inference (nullable) |
| `directives` | `DirectiveRegistry` | Active directives from players/Maestro |
| `battleCapability` | [BattleCapabilityProvider](BattleCapabilityProvider) | Generic battle readiness check |
| `position` | `Vec3d` | Current position of the persona |
| `homePosition` | `Vec3d` | Home position (spawn point / assigned base) |
| `world` | `ServerWorld` | The server world instance |
| `serverTick` | `long` | Current server tick count |

## Usage in evaluate()

```java
@Override
public Optional<ActionDecision> evaluate(ModuleContext ctx) {
    // Check environment
    if (ctx.environment().hasHostileWithin(8.0)) {
        return Optional.of(ActionDecision.flee(findSafePos(ctx)));
    }
    // Check inventory
    if (ctx.inventory().hasFood() && ctx.environment().food() < 6) {
        return Optional.of(ActionDecision.eat("hungry"));
    }
    return Optional.empty();
}
```

## Stability

Marked **API-SURFACE** — part of the public spp-lib API. Fields may be added in future versions but existing fields will not change type or be removed.
