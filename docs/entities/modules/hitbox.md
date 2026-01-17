---
sidebar_position: 2
---

# Hitbox

Configure the entity's collision box and eye height.

## Default Behavior

ModEngine uses sensible defaults that match vanilla Minecraft mobs:

| Dimension | Default | Behavior |
|-----------|---------|----------|
| **width** | `0.6` | Standard humanoid width (matches Zombie, Villager, Skeleton) |
| **height** | auto | Calculated from model geometry |
| **eye_height** | 85% | 85% of the final height |

This means entities can navigate through standard 1-block wide openings (like doors) without getting stuck.

:::tip Why not auto-calculate width?
Model bounds include arms, wings, and decorations that extend outward. Using these for collision would create hitboxes wider than the entity's "core body", causing navigation issues. Vanilla Minecraft uses a fixed 0.6 width for all humanoid mobs regardless of their visual size.
:::

## Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| copy | string | - | Copy hitbox from an existing entity (e.g., `minecraft:zombie`) |
| width | float | 0.6 | Width and depth in blocks |
| height | float | auto | Height in blocks |
| eye_height | float | 0.85 | Eye position height |

## Copying from Existing Entities

Use `copy` to match the exact hitbox of any registered entity:

```yaml
my_zombie:
  Model: custom_zombie
  Hitbox:
    copy: minecraft:zombie  # width: 0.6, height: 1.95
```

You can copy and then override specific values:

```yaml
tall_zombie:
  Model: tall_zombie
  Hitbox:
    copy: minecraft:zombie  # Get base dimensions
    height: 2.5             # Override just the height
```

### Common Entity Hitboxes

| Entity | Width | Height |
|--------|-------|--------|
| `minecraft:zombie` | 0.6 | 1.95 |
| `minecraft:skeleton` | 0.6 | 1.99 |
| `minecraft:spider` | 1.4 | 0.9 |
| `minecraft:creeper` | 0.6 | 1.7 |
| `minecraft:enderman` | 0.6 | 2.9 |
| `minecraft:iron_golem` | 1.4 | 2.7 |
| `minecraft:wolf` | 0.6 | 0.85 |
| `minecraft:chicken` | 0.4 | 0.7 |

## Manual Configuration

For precise control, specify values manually:

```yaml
my_entity:
  Hitbox:
    width: 0.8
    height: 2.0
    eye_height: 1.7
```

### Eye Height

The `eye_height` value can be:
- An absolute value (e.g., `1.7` = 1.7 blocks from ground)
- A ratio if less than 1.0 (e.g., `0.85` = 85% of height)

```yaml
# Absolute eye height
Hitbox:
  height: 2.0
  eye_height: 1.8  # 1.8 blocks up

# Ratio eye height
Hitbox:
  height: 2.0
  eye_height: 0.9  # 90% of 2.0 = 1.8 blocks up
```

## Examples

### Standard Humanoid
```yaml
custom_villager:
  Model: villager_model
  # No Hitbox needed - defaults work perfectly
  # width: 0.6 (default), height: auto from model
```

### Copy a Spider
```yaml
giant_spider:
  Model: spider_model
  Hitbox:
    copy: minecraft:spider
```

### Small Creature
```yaml
tiny_bug:
  Model: bug
  Hitbox:
    width: 0.3
    height: 0.2
    eye_height: 0.15
```

### Large Boss
```yaml
giant_boss:
  Model: boss_model
  Hitbox:
    width: 2.0
    height: 4.0
    eye_height: 3.5
```
