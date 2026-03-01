# Module Catalog

SPP ships with 5 core modules (M01-M05). All modules extend `AbstractModule`.

## M01 — EnvironmentSensorModule

| Property | Value |
|----------|-------|
| **ID** | `environment-sensor` |
| **Priority** | SAFETY |
| **Description** | Detects environmental hazards and triggers flee responses |

Monitors: lava proximity, cliff edges, drowning (air level), fire.

## M02 — InventoryModule

| Property | Value |
|----------|-------|
| **ID** | `inventory` |
| **Priority** | MAINTENANCE |
| **Description** | Manages inventory state and food consumption |

Monitors: inventory fullness, food availability, hunger level.

## M03 — ThreatModule

| Property | Value |
|----------|-------|
| **ID** | `threat` |
| **Priority** | SAFETY |
| **Description** | Detects nearby hostile mobs and triggers flee responses |

Monitors: hostile mobs within configurable radius, health-based threat assessment.

## M04 — SurvivalModule

| Property | Value |
|----------|-------|
| **ID** | `survival` |
| **Priority** | MAINTENANCE |
| **Description** | Handles eating and basic survival needs |

Triggers: hunger below threshold, health recovery needs.

## M05 — BuildModule

| Property | Value |
|----------|-------|
| **ID** | `build` |
| **Priority** | STANDBY |
| **Description** | Placeholder for future building behavior |

Status: Skeleton implementation, always returns empty decision.

## Module Priority Map

```
SAFETY:      M01 (EnvironmentSensor), M03 (Threat)
EXPLICIT:    (none — reserved for CahierDeReve directives)
MAINTENANCE: M02 (Inventory), M04 (Survival)
OBSERVED:    (none — reserved for auto-learning)
STANDBY:     M05 (Build)
```
