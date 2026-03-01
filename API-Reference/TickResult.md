# TickResult

`org.scentient.spp.persona.module.TickResult`

Returned by `PersonaModule.tick()` to indicate execution status.

## Values

| Value | Description |
|-------|-------------|
| `CONTINUE` | Module is still executing its decision. ActionEngine keeps ticking it. |
| `DONE` | Module completed its objective. ActionEngine re-evaluates next cycle. |
| `FAILED` | Module encountered an error or unrecoverable state. ActionEngine re-evaluates. |

## Usage

```java
@Override
public TickResult tick(PersonaEntity persona) {
    if (reachedTarget(persona)) {
        setActive(false);
        return TickResult.DONE;
    }
    if (isStuck(persona)) {
        setActive(false);
        return TickResult.FAILED;
    }
    return TickResult.CONTINUE;
}
```

## Stability

Marked **API-SURFACE** — part of the public spp-lib API.
