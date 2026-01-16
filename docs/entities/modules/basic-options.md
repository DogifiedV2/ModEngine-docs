---
sidebar_position: 1
---

# Basic Options

These are the core options for defining an entity.

## Model

**Required** - The model ID to use for this entity.

```yaml
my_entity:
  Model: example_model
```

The model ID corresponds to:
- A `.bbmodel` file: `models/example_model.bbmodel`
- Or a GeckoLib folder: `models/example_model/`

Model IDs are case-insensitive.

## Display

Custom display name shown above the entity. Supports color codes.

```yaml
my_entity:
  Display: '&c&lFire Demon'
```

**Color codes:**
- `&0`-`&f` - Colors (black to white)
- `&l` - Bold
- `&o` - Italic
- `&n` - Underline
- `&m` - Strikethrough
- `&k` - Obfuscated
- `&r` - Reset

See the [color codes reference](../../reference/color-codes) for all options.

## Health

Maximum health points. Default: `20.0`

```yaml
my_entity:
  Health: 100
```

The entity spawns with full health.

## Damage

Base attack damage. Default: `2.0`

```yaml
my_entity:
  Damage: 10
```

Only applies when the entity has an attack goal.

## Style

Applies procedural animation based on vanilla mob bone structures. Your model's bones must match the expected names.

```yaml
my_entity:
  Model: my_model
  Style: Zombie
```

**Available styles:**

| Style | Mobs |
|-------|------|
| Humanoid | Player, Zombie, Skeleton, Piglin, etc. |
| Quadruped | Pig, Cow, Wolf, Horse, etc. |
| Spider | Spider, Cave_Spider |
| Chicken | Chicken, Parrot |
| Creeper | Creeper |
| Villager | Villager, Witch, etc. |
| Iron_Golem | Iron_Golem |
| Snow_Golem | Snow_Golem |
| Slime | Slime, Magma_Cube |

See the [styles reference](../../reference/styles) for required bone names.

## Behavior

Preset AI behavior. This is ignored if `AIGoals` is specified.

```yaml
my_entity:
  Behavior: HOSTILE
```

**Available behaviors:**

| Behavior | Description |
|----------|-------------|
| `PASSIVE` | Wanders, doesn't attack |
| `HOSTILE` | Attacks players on sight |
| `NEUTRAL` | Attacks when provoked |
| `FLYING` | Passive with flying movement |
| `FLYING_HOSTILE` | Hostile with flying movement |

For custom AI, use [AIGoals](ai-goals) instead.

## Complete Example

```yaml
fire_zombie:
  Model: fire_zombie
  Display: '&c&lFire Zombie'
  Health: 40
  Damage: 8
  Style: Zombie
  Behavior: HOSTILE
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
    - animation{name=attack} ~onHurt
```
