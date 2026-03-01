# BattleCapabilityProvider

`org.scentient.spp.api.BattleCapabilityProvider`

Generic capability check for battle readiness. This is a `@FunctionalInterface` — can be implemented as a lambda or method reference.

## Method

### `boolean canBattle(UUID agentUuid)`
Returns whether the agent with the given UUID can engage in battle. Implementations:

- **CobblemonAdapter**: Checks if the Pokemon party has at least one non-fainted member
- **NoOpCobblemonAdapter**: Always returns `true` (no Cobblemon installed)
- **Lambda**: `uuid -> true` for testing

## Usage in ModuleContext

```java
@Override
public Optional<ActionDecision> evaluate(ModuleContext ctx) {
    if (!ctx.battleCapability().canBattle(ctx.personaUuid())) {
        return Optional.of(ActionDecision.seekHeal());
    }
    return Optional.empty();
}
```

## Design

This interface lives in `org.scentient.spp.api` — the package that will form the public spp-lib API. It decouples the module system from Cobblemon-specific code, allowing modules to check battle readiness without importing Cobblemon classes.

## Stability

Marked **API-SURFACE** — part of the public spp-lib API.
