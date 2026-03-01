# Getting Started

## Prerequisites

- Java 21
- Minecraft 1.21.1
- Fabric Loader 0.18.4
- Carpet Mod (required for FakePlayer support)
- PrismLauncher (recommended for client)

## Dev Environment Setup

1. Clone the repository:
   ```bash
   git clone git@github.com:firefloc/spp-ai.git
   cd spp-ai
   ```

2. Build the mod:
   ```bash
   ./gradle-local.sh --no-daemon build -x test
   ```

3. Start the dev server:
   ```bash
   ./scripts/dev-start.sh
   ```
   This script:
   - Builds the JAR
   - Copies it to the standalone server (`run/server/mods/`)
   - Copies it to PrismLauncher SPP-Dev instance
   - Starts the standalone server with Java 21

4. Connect with PrismLauncher:
   - Instance: SPP-Dev
   - Server: `127.0.0.1:25565`

## Important Notes

- **Do NOT use `gradle runServer`** — Cobblemon crashes due to Kotlin Reflect bypassing Loom remapper
- **Do NOT use `gradle runClient`** — Cobblemon mixins fail (namespace mismatch)
- Always use the standalone server + PrismLauncher approach

## First Steps

1. Connect to the dev server
2. Try `/spp help` to see all available commands
3. Try `/spp status` to see active agents
4. Try `/spp npc spawn` to create an autonomous NPC

## Enabling Dev Tests

Dev tests are hidden by default. To enable:
1. Edit `config/spp/spp-persona.json`
2. Set `"enableDevTests": true`
3. Restart the server
4. `/spp test brick6` runs the module system autotest
