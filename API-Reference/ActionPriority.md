# ActionPriority

`org.scentient.spp.persona.module.ActionPriority`

Priority levels matching ActionEngine's evaluation order. Modules register at a priority level; ActionEngine iterates from highest to lowest.

## Values (highest to lowest)

| Priority | Description | Example |
|----------|-------------|---------|
| `SAFETY` | Immediate hazard response (lava, fire, void, drowning) | ThreatModule |
| `EXPLICIT` | Player-issued commands (CahierDeReve, directives) | — |
| `MAINTENANCE` | Self-preservation (eat, heal Pokemon) | SurvivalModule |
| `OBSERVED` | Learned behavior patterns | — |
| `STANDBY` | Default behavior when nothing else triggers | BuildModule |

## Evaluation Rule

ActionEngine evaluates all enabled modules at each priority level, highest first. The **first non-empty** `Optional<ActionDecision>` wins. Lower priorities are skipped entirely.

## Stability

Marked **API-SURFACE** — part of the public spp-lib API. Values are stable; new values may be added between existing ones in future versions.
