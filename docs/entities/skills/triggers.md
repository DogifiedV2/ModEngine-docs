---
sidebar_position: 4
---

# Triggers

Triggers determine when a skill activates. There are three types: event triggers, state triggers, and pet triggers.

## Event Triggers

Fire once when an event occurs.

### ~onSpawn

Fires when the entity spawns.

```yaml
Skills:
  - animation{name=spawn} ~onSpawn
```

### ~onDeath

Fires when the entity dies.

```yaml
Skills:
  - animation{name=death} ~onDeath
  - damage{amount=10, type=explosion} @PlayersInRadius{r=5} ~onDeath
```

### ~onHurt

Fires when the entity takes damage.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| min | number | 0 | Minimum damage to trigger |
| max | number | infinity | Maximum damage to trigger |
| once | boolean | false | Only trigger once ever |

```yaml
Skills:
  # Any damage
  - animation{name=hurt} ~onHurt

  # Heavy hits only (10+ damage)
  - animation{name=big_hit} ~onHurt{min=10}

  # Light hits only (under 5 damage)
  - animation{name=flinch} ~onHurt{max=5}

  # First time hurt only
  - animation{name=surprised} ~onHurt{once=true}
```

## State Triggers

Active continuously while a condition is true.

### ~idle

Fires while the entity is not moving.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| threshold | number | 0.01 | Speed threshold for idle |
| time | number | 0 | Seconds idle before triggering |
| maxTime | number | -1 | Max seconds (-1 = forever) |
| once | boolean | false | Only trigger once per idle |

```yaml
Skills:
  # Basic idle
  - animation{name=idle, mode=loop} ~idle

  # Sleep after 5 seconds of idle
  - animation{name=sleep, mode=hold} ~idle{time=5}

  # Idle for max 5 seconds, then do something else
  - animation{name=idle, mode=loop} ~idle{maxTime=5}
  - animation{name=bored, mode=loop} ~idle{time=5}
```

### ~moving

Fires while the entity is moving.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | number | 0.01 | Minimum speed threshold |

```yaml
Skills:
  # Basic walk
  - animation{name=walk, mode=loop} ~moving

  # Run when moving fast
  - animation{name=run, mode=loop} ~moving{speed=0.3}
  - animation{name=walk, mode=loop} ~moving
```

### ~health

Fires based on health percentage.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| below | number | 100 | Trigger when health below this % |
| above | number | 0 | Trigger when health above this % |
| once | boolean | false | Only trigger once |

```yaml
Skills:
  # Enrage at half health (once)
  - animation{name=enrage} ~health{below=50, once=true}

  # Critical state under 25%
  - animation{name=desperate, mode=loop} ~health{below=25}

  # Between 25% and 50%
  - animation{name=wounded, mode=loop} ~health{below=50, above=25}

  # Trigger ability once at 50%
  - damage{amount=10} @PlayersInRadius{r=8} ~health{below=50, once=true}
```

## Pet Triggers

Require the [Taming](../taming) module.

### ~tamed

Fires while the entity is tamed.

```yaml
Skills:
  - animation{name=happy, mode=loop} ~tamed
```

### ~untamed

Fires while the entity is not tamed.

```yaml
Skills:
  - animation{name=wary, mode=loop} ~untamed
```

### ~sitting

Fires while the entity is ordered to sit. Requires `can_sit: true` in Taming.

```yaml
Skills:
  - animation{name=sit, mode=hold} ~sitting
```

## Complete Examples

### Standard Mob
```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
  - animation{name=hurt} ~onHurt
  - animation{name=death} ~onDeath
```

### Boss with Phases
```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
  - animation{name=spawn} ~onSpawn

  # Phase 2 at 66%
  - animation{name=phase2_transform} ~health{below=66, once=true}
  - showbone{bone=phase2_armor} ~health{below=66, once=true}

  # Phase 3 at 33%
  - animation{name=phase3_transform} ~health{below=33, once=true}
  - showbone{bone=phase3_wings} ~health{below=33, once=true}
  - damage{amount=10, type=magic} @PlayersInRadius{r=12} ~health{below=33, once=true}

  # Death
  - damage{amount=20, type=explosion} @PlayersInRadius{r=10} ~onDeath
```

### Pet with States
```yaml
Taming:
  item: minecraft:bone
  chance: 0.33

Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
  - animation{name=sit, mode=hold} ~sitting
  - animation{name=happy, mode=loop} ~tamed
  - animation{name=wary, mode=loop} ~untamed
  - animation{name=sleep, mode=hold} ~idle{time=10}
```
