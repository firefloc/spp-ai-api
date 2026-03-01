# Command Reference

All commands are under the `/spp` root. Permission levels: (empty) = any player, [op] = requires operator level 2.

## General

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp help` | Display help | |
| `/spp status` | List active Personas and agents | [op] |

## NPC Management

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp npc spawn` | Spawn autonomous NPC (default: Guide, radius 24) | [op] |
| `/spp npc spawn <name>` | Spawn NPC with custom name | [op] |
| `/spp npc spawn <name> <radius>` | Spawn with name and patrol radius | [op] |
| `/spp npc spawn <name> <radius> <role>` | Roles: trainer, lumberjack, patrol | [op] |
| `/spp npc role <target> <role>` | Change active NPC's role | [op] |
| `/spp npc challenge <target>` | Challenge a trainer NPC to Pokemon battle | |
| `/spp npc stop <target>` | Stop and despawn an NPC by name | [op] |
| `/spp npc stopall` | Stop all autonomous NPCs | [op] |
| `/spp npc list` | List active autonomous NPCs | [op] |
| `/spp npc debug` | Show NPC state machine internals | [op] |

## View (POV)

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp view start <target>` | Observe a Persona's point of view | |
| `/spp view stop` | Exit observation mode | |
| `/spp view list` | List active view links | [op] |

## Pilot

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp pilot start <target>` | Take control of a Persona's movement | |
| `/spp pilot stop` | Release Persona control | |
| `/spp pilot list` | List active pilot links | [op] |

## Scenario

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp scenario run <text>` | Run scenario: `role:<r> name:<n> objective:<o>` | [op] |
| `/spp scenario status` | Show running scenarios | [op] |

## RCT Control

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp control bind <trainerId>` | Bind an RCT trainer to SPP control | [op] |
| `/spp control battle <trainerId> <player>` | Trigger battle between RCT trainer and player | [op] |
| `/spp control snapshot <trainerId>` | Show RCT trainer state | [op] |

## Cahier de Reves

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp cahier` | Open the Cahier de Reves (instruction book) | |
| `/spp cahier clear` | Clear the Cahier de Reves | |
| `/spp cahier show` | Display content and parsed directive | |

## Directives

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp directive set <target> <type> [x y z]` | Inject a directive (patrol, moveto, idle, retreat) | [op] |
| `/spp directive clear <target>` | Clear an agent's directive | [op] |

## Maestro

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp maestro` | Show active zones and directives | [op] |

## Module System

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp module list` | List all modules and their state | [op] |
| `/spp module enable <id>` | Enable a behavior module | [op] |
| `/spp module disable <id>` | Disable a behavior module | [op] |
| `/spp module reload` | Reload all module JSON configs | [op] |
| `/spp module info <id>` | Show module details and config | [op] |

## Debug

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp debug <name>` | Toggle verbose navigation debug for an NPC/probe | [op] |

## Dev Tests (hidden by default)

Requires `enableDevTests: true` in `config/spp/spp-persona.json`.

| Command | Description | Permission |
|---------|-------------|------------|
| `/spp test start [count]` | Launch N autonomous navigation probes | [op] |
| `/spp test stop` | Stop and despawn all probes | [op] |
| `/spp test brick1` | Autotest: RCT config + surface + scan + bind + state store | [op] |
| `/spp test brick2` | Autotest: Persona surface + spawn + move + snapshot + despawn | [op] |
| `/spp test brick3` | Autotest: ActionEngine priority stack + handover | [op] |
| `/spp test brick4` | Autotest: DirectiveRegistry + Maestro + ActionLog | [op] |
| `/spp test brick5` | Autotest: CahierDeReve + OBSERVED + SEEK_HEAL | [op] |
| `/spp test brick6` | Autotest: ModuleRegistry + 5 modules + ThreatModule eval | [op] |
