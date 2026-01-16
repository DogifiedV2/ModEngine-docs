---
sidebar_position: 5
---

# Taming

Enable pet-like behavior for entities. Tamed entities follow their owner and can be commanded to sit.

## Basic Usage

```yaml
my_pet:
  Model: pet_model
  Display: '&ePet'
  Taming:
    item: minecraft:bone
    chance: 0.33
```

## Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| item | string | minecraft:bone | Item used to tame |
| chance | float | 0.33 | Success chance per use (0-1) |
| follow_distance | float | 10.0 | Distance to start following |
| stop_distance | float | 2.0 | Distance to stop following |
| teleport_distance | float | 12.0 | Distance to teleport to owner |
| can_sit | boolean | true | Can be ordered to sit |
| follow_speed | float | 1.0 | Speed multiplier when following |

## Behavior

### Taming Process
- Use the configured item on an untamed entity
- Each use has a `chance` probability of success
- Hearts appear on success, smoke on failure
- Once tamed, the entity belongs to that player

### Following
- Follows owner when `follow_distance` blocks away
- Stops when within `stop_distance` blocks
- Teleports if owner exceeds `teleport_distance`
- Won't follow while sitting

### Sitting
- Right-click a tamed entity to toggle sitting
- While sitting, stays in place
- Requires `can_sit: true`

## Default AI

Without `AIGoals`, tamed entities automatically get:
1. SitWhenOrdered
2. FollowOwner
3. Float
4. LookAtPlayer
5. RandomLookAround

Specify `AIGoals` for full control.

## Pet Triggers

Use these in [Skills](../skills/overview) for taming-specific animations:

| Trigger | Description |
|---------|-------------|
| `~tamed` | While entity is tamed |
| `~untamed` | While entity is not tamed |
| `~sitting` | While entity is sitting |

## Examples

### Basic Pet
```yaml
pet_wolf:
  Model: wolf
  Display: '&7Pet Wolf'
  Type: Wolf
  Taming:
    item: minecraft:bone
    chance: 0.33
```

### Rare Tame
```yaml
pet_dragon:
  Model: dragon_hatchling
  Display: '&5Baby Dragon'
  Taming:
    item: minecraft:dragon_breath
    chance: 0.1
    follow_distance: 15.0
    teleport_distance: 20.0
    follow_speed: 1.5
```

### Pet with Animations
```yaml
pet_fox:
  Model: custom_fox
  Display: '&6Tamed Fox'
  Taming:
    item: minecraft:sweet_berries
    chance: 0.25
    can_sit: true
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
    - animation{name=sit, mode=hold} ~sitting
    - animation{name=happy, mode=loop} ~tamed
    - animation{name=wary, mode=loop} ~untamed
```

### Pet with Sleep
```yaml
husky:
  Model: husky
  Display: '&fHusky'
  Taming:
    item: minecraft:bone
    chance: 0.33
    can_sit: true
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=run, mode=loop} ~moving
    - animation{name=sit, mode=hold} ~sitting
    - animation{name=sleep, mode=hold} ~idle{time=5, once=true}
```
