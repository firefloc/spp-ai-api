# AbstractModule

`org.scentient.spp.persona.module.AbstractModule`

Base class for internal modules providing default implementations for enabled/active state management and cancel logic. Subclasses only need to implement `id()`, `priority()`, `evaluate()`.

## Default Behavior

| Method | Default |
|--------|---------|
| `isEnabled()` | `true` |
| `loadConfig(JsonObject)` | No-op |
| `tick(PersonaEntity)` | Returns `TickResult.DONE` (one-shot decisions) |
| `cancel()` | Sets active to `false` |
| `isActive()` | Returns current active state |

## Protected API

### `void setActive(boolean active)`
Subclasses call this to mark themselves as actively executing a multi-tick decision.

## Usage

Extend `AbstractModule` for most modules. Only implement `PersonaModule` directly if you need full control over all lifecycle methods.

```java
public class PatrolModule extends AbstractModule {
    @Override
    public String id() { return "patrol"; }

    @Override
    public ActionPriority priority() { return ActionPriority.STANDBY; }

    @Override
    public Optional<ActionDecision> evaluate(ModuleContext ctx) {
        // Patrol logic here
        return Optional.of(ActionDecision.moveTo(target, "patrol"));
    }
}
```

## Stability

Marked **API-SURFACE** — part of the public spp-lib API.
