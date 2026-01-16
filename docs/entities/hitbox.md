---
sidebar_position: 3
---

# Hitbox

Configure the entity's collision box and eye height.

## Auto-Detection

If `Hitbox` is not specified, ModEngine automatically calculates the hitbox from your model's geometry. This works for both Blockbench and GeckoLib models.

The auto-detection:
- Transforms all cube vertices through the bone hierarchy
- Finds the bounding box of all geometry
- Sets eye height to 85% of the total height

## Manual Configuration

For precise control, specify the hitbox manually:

```yaml
my_entity:
  Hitbox:
    width: 0.8
    height: 2.0
    eye_height: 1.7
```

## Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| width | float | auto | Width and depth in blocks |
| height | float | auto | Height in blocks |
| eye_height | float | 0.85 | Eye position height |

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

### Let Auto-Detection Handle It
```yaml
auto_sized:
  Model: my_model
  # No Hitbox specified - calculated from model
```
