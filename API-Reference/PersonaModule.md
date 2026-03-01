# PersonaModule

`org.scentient.spp.persona.module.PersonaModule`

Core interface for all behavior modules in the SPP system. A module provides decisions at a specific priority level in the ActionEngine stack. The ActionEngine iterates modules by priority (SAFETY first, STANDBY last). First module to return a non-empty decision wins that evaluation cycle.

## Lifecycle

```
register() → loadConfig() → evaluate() → tick() → cancel()
```

1. **register()** — Module added to ModuleRegistry at server startup
2. **loadConfig(JsonObject)** — Module reads its JSON config from `config/spp/behavior/{id}.json`
3. **evaluate(ModuleContext)** — Called each ActionEngine cycle, returns `Optional<ActionDecision>`
4. **tick(PersonaEntity)** — Called each server tick while this module's decision is active
5. **cancel()** — Called when a higher-priority module preempts this one

## Methods

### `String id()`
Unique identifier matching the config filename (`config/spp/behavior/{id}.json`).

### `ActionPriority priority()`
Priority level where this module's decisions are evaluated. See [ActionPriority](ActionPriority).

### `void loadConfig(JsonObject config)`
Load module-specific configuration from a parsed JSON object. May receive `null` if no config file exists.

### `boolean isEnabled()`
Whether this module is currently enabled (can be toggled at runtime via `/spp module enable/disable`).

### `void setEnabled(boolean enabled)`
Enable or disable this module.

### `Optional<ActionDecision> evaluate(ModuleContext ctx)`
Evaluate whether this module has a decision to propose. Called once per ActionEngine evaluation cycle (every N ticks). **Must be fast (< 1ms)** — never block the server thread.

**Parameters:** `ctx` — the current world context snapshot (see [ModuleContext](ModuleContext))
**Returns:** a decision if this module wants to act, empty otherwise

### `TickResult tick(PersonaEntity persona)`
Execute the module's active decision each server tick. Only called when this module's decision was chosen by ActionEngine.

**Returns:** `CONTINUE` if still executing, `DONE` if finished, `FAILED` if aborted. See [TickResult](TickResult).

### `void cancel()`
Cancel the current execution (preempted by higher-priority module).

### `boolean isActive()`
Returns true if this module is currently executing a decision.

### `String description()` *(default)*
Human-readable description for `/spp module info`. Default: `"(no description)"`.

## Example

```java
public class MyModule extends AbstractModule {
    @Override
    public String id() { return "my-module"; }

    @Override
    public ActionPriority priority() { return ActionPriority.OBSERVED; }

    @Override
    public Optional<ActionDecision> evaluate(ModuleContext ctx) {
        if (ctx.environment().isNight() && ctx.environment().health() < 10) {
            return Optional.of(ActionDecision.idle("night-low-health"));
        }
        return Optional.empty();
    }

    @Override
    public String description() { return "Idles at night when health is low"; }
}
```

## Stability

This interface is marked **API-SURFACE** — it will be part of the public spp-lib API. Method signatures are considered stable.
