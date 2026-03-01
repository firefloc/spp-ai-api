# WorldSnapshot

`org.scentient.spp.persona.module.WorldSnapshot`

Immutable snapshot of the world around a Persona at a given tick. Computed once per evaluation cycle, shared across all modules. All fields are final — no side effects, safe to read from any context.

## Fields

| Field | Type | Description |
|-------|------|-------------|
| `timeOfDay` | `long` | Game time 0-24000 ticks |
| `isNight` | `boolean` | True if `timeOfDay > 13000` |
| `isRaining` | `boolean` | Weather: rain |
| `isThundering` | `boolean` | Weather: thunderstorm |
| `lightLevel` | `int` | Block light at feet position |
| `skyLightLevel` | `int` | Sky light at feet (0 = cave) |
| `biomeKey` | `String` | e.g. `"minecraft:plains"` |
| `isInCave` | `boolean` | `skyLightLevel == 0` AND solid block above |
| `isUnderwater` | `boolean` | Feet in water |
| `health` | `float` | 0-20 (hearts) |
| `food` | `int` | 0-20 (hunger bar) |
| `air` | `int` | Remaining air ticks (0-300) |
| `nearbyHostiles` | `List<EntityEntry>` | Hostile mobs near the persona |
| `nearbyPlayers` | `List<EntityEntry>` | Players near the persona |
| `nearLava` | `boolean` | Lava within 5 blocks |
| `nearCliff` | `boolean` | Drop of 4+ blocks within 3 blocks |
| `position` | `Vec3d` | Position at scan time |

## Inner Record: EntityEntry

| Field | Type | Description |
|-------|------|-------------|
| `type` | `String` | e.g. `"zombie"`, `"skeleton"`, `"player"` |
| `position` | `Vec3d` | Entity position |
| `distance` | `double` | Distance from persona |
| `health` | `float` | Entity health |

## Convenience Methods

### `boolean hasHostileWithin(double radius)`
True if any hostile mob is within the given radius.

### `int hostileCountWithin(double radius)`
Count of hostile mobs within the given radius.

## Stability

Marked **API-SURFACE** — part of the public spp-lib API. Fields may be added in future versions.
