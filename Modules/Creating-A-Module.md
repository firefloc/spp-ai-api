# Creating a Module

Step-by-step guide to creating a custom behavior module for SPP.

## Step 1: Create the Class

Create a new class that extends `AbstractModule`:

```java
package org.scentient.spp.persona.module;

import org.scentient.spp.persona.ActionDecision;
import java.util.Optional;

public class NightShelterModule extends AbstractModule {

    @Override
    public String id() {
        return "night-shelter";
    }

    @Override
    public ActionPriority priority() {
        return ActionPriority.OBSERVED;
    }

    @Override
    public Optional<ActionDecision> evaluate(ModuleContext ctx) {
        // Only act at night when outdoors
        if (!ctx.environment().isNight() || ctx.environment().isInCave()) {
            return Optional.empty();
        }

        // Seek shelter (go home)
        if (ctx.position().squaredDistanceTo(ctx.homePosition()) > 100) {
            return Optional.of(ActionDecision.moveTo(ctx.homePosition(), "night-go-home"));
        }

        return Optional.of(ActionDecision.idle("night-at-home"));
    }

    @Override
    public String description() {
        return "Returns home at night for safety";
    }
}
```

## Step 2: Create the JSON Config (Optional)

Create `config/spp/behavior/night-shelter.json`:

```json
{
  "enabled": true,
  "shelterRadius": 64,
  "nightStartTick": 13000
}
```

Override `loadConfig()` to read custom settings:

```java
@Override
public void loadConfig(JsonObject config) {
    if (config != null && config.has("shelterRadius")) {
        this.shelterRadius = config.get("shelterRadius").getAsInt();
    }
}
```

## Step 3: Register the Module

In `PersonaManager.onServerStart()`, add:

```java
moduleRegistry.register(new NightShelterModule());
```

## Step 4: Test

1. Build: `./gradle-local.sh --no-daemon build -x test`
2. Start server: `./scripts/dev-start.sh`
3. Check registration: `/spp module list`
4. Check details: `/spp module info night-shelter`
5. Toggle: `/spp module disable night-shelter` / `/spp module enable night-shelter`

## Key Rules

- **evaluate() must be fast** — under 1ms, never block the server thread
- **No state mutation in evaluate()** — the ModuleContext is read-only
- **Use factory methods** — `ActionDecision.moveTo()`, `.flee()`, `.idle()`, etc.
- **One decision per cycle** — return `Optional.empty()` if nothing to do
- **Multi-tick via tick()** — override `tick()` and return `TickResult.CONTINUE` for ongoing actions
