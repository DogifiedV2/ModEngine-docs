---
sidebar_position: 4
---

# AI Goals

Define custom AI behavior for your entity. When `AIGoals` is present, it overrides any `Behavior` preset.

## Syntax

Each goal can be simple or have parameters:

```yaml
AIGoals:
  - float                           # Simple
  - meleeattack{speed=1.2}          # With parameters
  - randomstroll{speed=0.8}
```

## Goal Types

### float

Keeps the entity above water.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 0

```yaml
- float
```

### panic

Makes the entity flee when hurt.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.25 | Movement speed while fleeing |

**Priority:** 1

```yaml
- panic
- panic{speed=1.5}
```

### meleeattack

Performs melee attacks on the current target.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.0 | Chase speed |
| alwaysfollow | boolean | false | Follow through walls |
| priority | int | 2 | Goal priority |

**Priority:** 2

```yaml
- meleeattack
- meleeattack{speed=1.2, alwaysfollow=true}
```

:::note
If you have attack goals but no `AITargets`, the entity defaults to `hurtbytarget` (only attacks when attacked first).
:::

### randomstroll

Wanders randomly when idle.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 0.8 | Wander speed |

**Priority:** 7

```yaml
- randomstroll
- randomstroll{speed=0.5}
```

### lookatplayer

Looks at nearby players.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| range | double | 8.0 | Look range in blocks |

**Priority:** 8

```yaml
- lookatplayer
- lookatplayer{range=12.0}
```

## Priority System

Goals execute based on priority (lower number = higher priority):

| Priority | Goal |
|----------|------|
| 0 | float |
| 1 | panic |
| 2 | meleeattack |
| 7 | randomstroll |
| 8 | lookatplayer |

Override priority on any goal:

```yaml
- meleeattack{priority=1}  # Higher priority than default
```

## Examples

### Passive Mob
```yaml
AIGoals:
  - float
  - randomstroll{speed=0.6}
  - lookatplayer
```

### Hostile Mob
```yaml
AIGoals:
  - float
  - meleeattack{speed=1.2}
  - randomstroll
  - lookatplayer
AITargets:
  - nearestplayer
```

### Neutral Mob
```yaml
AIGoals:
  - float
  - meleeattack
  - randomstroll
  - lookatplayer
AITargets:
  - hurtbytarget
```

### Cowardly Mob
```yaml
AIGoals:
  - float
  - panic{speed=1.5}
  - randomstroll{speed=0.4}
  - lookatplayer
```
