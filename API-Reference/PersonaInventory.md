# PersonaInventory

`org.scentient.spp.persona.module.PersonaInventory`

Utility class wrapping a FakePlayer's inventory for module queries. All methods are pure reads — no inventory modification. Created per-evaluation cycle from the PersonaEntity's FakePlayer.

## Methods

### `int usedSlots()`
Returns the number of non-empty inventory slots.

### `boolean isInventoryFull()`
Returns true if inventory has 35+ non-empty slots.

### `int scaffoldBlockCount()`
Returns total count of solid blocks suitable for scaffolding/bridging (cobblestone, dirt, stone, planks variants, etc.).

### `boolean hasScaffoldBlocks(int count)`
Returns true if the player has at least `count` scaffold blocks.

### `ItemStack findScaffoldBlock()`
Returns the first scaffold block stack found, or `ItemStack.EMPTY`.

### `boolean hasFood()`
Returns true if the player has food items.

### `ItemStack findFood()`
Returns the first food item found, or `ItemStack.EMPTY`.

### `ServerPlayerEntity getPlayer()`
Returns the underlying player (for advanced module use).

## Stability

Marked **API-SURFACE** — part of the public spp-lib API.
