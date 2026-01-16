---
sidebar_position: 4
---

# AI Targets

Define what entities your mob will target for attacks.

## Syntax

```yaml
AITargets:
  - nearestplayer
  - hurtbytarget{alertallies=true}
```

## Target Types

### nearestplayer

Targets the nearest player within range.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 1

```yaml
- nearestplayer
```

### hurtbytarget

Targets whatever entity last attacked this mob.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| alertallies | boolean | false | Alert nearby mobs of the same type |

**Priority:** 2

```yaml
- hurtbytarget
- hurtbytarget{alertallies=true}
```

## Priority System

Targets are checked based on priority (lower = checked first):

| Priority | Target |
|----------|--------|
| 1 | nearestplayer |
| 2 | hurtbytarget |

Override with:
```yaml
- hurtbytarget{priority=1}
- nearestplayer{priority=2}
```

## Examples

### Hostile
Attacks players on sight:
```yaml
AITargets:
  - nearestplayer
```

### Neutral
Only attacks when provoked:
```yaml
AITargets:
  - hurtbytarget
```

### Hostile + Retaliates
Attacks players and retaliates against other attackers:
```yaml
AITargets:
  - nearestplayer
  - hurtbytarget
```

### Pack Animal
Alerts allies when attacked:
```yaml
AITargets:
  - hurtbytarget{alertallies=true}
```

## Complete Example

```yaml
pack_wolf:
  Model: wolf_model
  Display: '&7Pack Wolf'
  Health: 20
  Damage: 4
  AIGoals:
    - float
    - meleeattack{speed=1.3}
    - randomstroll
    - lookatplayer
  AITargets:
    - hurtbytarget{alertallies=true}
```
