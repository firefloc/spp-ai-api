# Module Configuration

Modules load their configuration from JSON files in `config/spp/behavior/`.

## File Location

```
config/spp/behavior/{module-id}.json
```

Each module's `id()` determines its config filename. For example, module `"threat"` reads from `config/spp/behavior/threat.json`.

## Config Loading

1. At server startup, `ModuleRegistry.loadAll()` iterates all registered modules
2. For each module, it looks for `config/spp/behavior/{id}.json`
3. If the file exists, it's parsed as a `JsonObject` and passed to `loadConfig()`
4. If the file doesn't exist, `loadConfig(null)` is called (modules should handle null gracefully)

## Common Pattern

```json
{
  "enabled": true,
  "customParam1": 10,
  "customParam2": "value"
}
```

Modules typically read `enabled` in `loadConfig()` and call `setEnabled()`:

```java
@Override
public void loadConfig(JsonObject config) {
    if (config != null && config.has("enabled")) {
        setEnabled(config.get("enabled").getAsBoolean());
    }
}
```

## Runtime Reload

Use `/spp module reload` to reload all module configs from disk without restarting the server.

## Global Config

The global persona config is at `config/spp/spp-persona.json` and controls:
- `actionEngineEvalInterval` — ticks between re-evaluations (default: 20)
- `actionLogMaxEntries` — max entries in action log (default: 200)
- `maestroTickInterval` — ticks between Maestro zone recalculations (default: 200)
- `enableDevTests` — show/hide `/spp test` commands (default: false)

See `SppPersonaConfig` for the full list of fields.
