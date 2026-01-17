---
sidebar_position: 9
---

# Drops

Configure custom loot drops when an entity dies. Supports items, commands, experience, and disabling default drops.

## Syntax

```yaml
Drops:
  - <type> <amount> <probability>
```

Where:
- `type` - Drop type: item ID, `cmd{...}`, `exp`, or `nothing`
- `amount` - Amount to drop (or range like `1to5`)
- `probability` - Either a chance (0.0-1.0) or a weight (integer)

## Probability Modes

### Chance Mode

When the probability is a decimal (has a `.`), each drop is rolled independently:

```yaml
Drops:
  - diamond 1 0.2       # 20% chance to drop 1 diamond
  - gold_ingot 3 0.5    # 50% chance to drop 3 gold ingots
  - emerald 1 0.1       # 10% chance to drop 1 emerald
```

All three drops are rolled separately, so the entity could drop any combination.

### Weight Mode

When the probability is an integer (no `.`), one drop is selected randomly based on weights:

```yaml
Drops:
  - diamond 1 10        # 10/100 = 10% chance
  - gold_ingot 3 30     # 30/100 = 30% chance
  - emerald 1 60        # 60/100 = 60% chance
```

Only one drop is selected from the pool.

:::warning
Do not mix chance and weight modes in the same Drops list. Choose one mode and use it consistently.
:::

---

## Drop Types

### Items

Drop any Minecraft item. Amount can be a fixed number or a range.

```yaml
Drops:
  - diamond 3 0.2               # 3 diamonds with 20% chance
  - minecraft:gold_ingot 5 0.5  # Full namespace also works
  - iron_ingot 1to5 0.3         # Random 1-5 iron ingots, 30% chance
```

### Commands

Execute a command when the drop is triggered. Commands run as console with operator permissions.

```yaml
Drops:
  - cmd{c="give <trigger.name> diamond 1"} 1 0.5
```

#### Command Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `c` | **required** | The command to execute |
| `asconsole` | `true` | Run as console (true) or as the killer (false) |

#### Placeholders

| Placeholder | Description |
|-------------|-------------|
| `<trigger.name>` | Name of the player/entity who killed the mob |
| `<trigger.uuid>` | UUID of the killer |
| `<trigger.x>`, `<trigger.y>`, `<trigger.z>` | Killer's position |
| `<entity.name>` | Name of the dying entity |
| `<entity.uuid>` | UUID of the dying entity |
| `<entity.x>`, `<entity.y>`, `<entity.z>` | Entity's death position |
| `<killer.name>` | Alias for `<trigger.name>` |

#### Command Examples

```yaml
Drops:
  # Give a custom item via another mod
  - cmd{c="crate give <trigger.name> RewardCrate 1"} 1 0.2

  # Run a custom command at the entity's location
  - cmd{c="summon lightning_bolt <entity.x> <entity.y> <entity.z>"} 1 0.1

  # Grant player a title/achievement
  - cmd{c="title <trigger.name> title {\"text\":\"Boss Slain!\"}"} 1 1.0
```

### Experience

Drop experience orbs. Amount can be a fixed number or a range.

```yaml
Drops:
  - exp 50 0.8             # 50 XP with 80% chance
  - exp 100to500 0.5       # Random 100-500 XP with 50% chance
  - xp 200 1.0             # 'xp' also works
```

### Nothing

Disables all vanilla drops (items, equipment, and experience). Custom drops in the same list still work.

```yaml
Drops:
  - nothing                # Disable vanilla drops
  - diamond 1 0.3          # Still drops diamond with 30% chance
```

---

## Examples

### Basic Boss Drops

```yaml
fire_dragon:
  Model: dragon
  Health: 200
  Damage: 15
  Drops:
    - nothing              # No vanilla drops
    - diamond 3to5 0.8     # 3-5 diamonds, 80% chance
    - nether_star 1 0.1    # Nether star, 10% chance
    - exp 500to1000 1.0    # Always drop 500-1000 XP
```

### Weighted Loot Table

```yaml
treasure_mimic:
  Model: chest
  Health: 50
  Drops:
    - nothing
    - diamond 1 10               # 10% chance (rare)
    - gold_ingot 3 25            # 25% chance (uncommon)
    - iron_ingot 5 40            # 40% chance (common)
    - coal 8 25                  # 25% chance (common)
```

### Reward Crate Integration

```yaml
dungeon_boss:
  Model: boss_model
  Health: 500
  Drops:
    - nothing
    - cmd{c="crate give <trigger.name> BossCrate 1"} 1 1.0
    - exp 1000 1.0
```

### Multiple Chance Drops

```yaml
elite_skeleton:
  Model: humanoid
  Preset: skeleton
  Health: 40
  Drops:
    - bone 2to4 0.9        # Very likely
    - arrow 5to10 0.7      # Likely
    - bow 1 0.2            # Rare
    - diamond 1 0.05       # Very rare
```

---

## Notes

- Commands are executed server-side only
- If no killer exists (e.g., environmental death), killer placeholders resolve to empty strings or entity position
- The `amount` field for `cmd` drops is ignored (use `1`)
- Drops execute after death skills but during the loot drop phase
