---
sidebar_position: 4
---

# ~idle

Fires while the entity is not moving.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| threshold | number | 0.01 | Speed threshold for idle detection |
| time | number | 0 | Seconds idle before triggering |
| maxTime | number | -1 | Max seconds to stay triggered (-1 = forever) |
| once | boolean | false | Only trigger once per idle period |

## Examples

```yaml
Skills:
  # Basic idle
  - animation{name=idle, mode=loop} ~idle

  # Sleep after 5 seconds of idle
  - animation{name=sleep, mode=hold} ~idle{time=5}

  # Idle for max 5 seconds, then switch
  - animation{name=idle, mode=loop} ~idle{maxTime=5}
  - animation{name=bored, mode=loop} ~idle{time=5}
```

## Common Patterns

### Basic Idle
```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
```

### Idle to Sleep Transition
```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle{maxTime=10}
  - animation{name=drowsy, mode=loop} ~idle{time=10, maxTime=15}
  - animation{name=sleep, mode=hold} ~idle{time=15}
```

### Bored Animation
```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle{maxTime=8}
  - animation{name=yawn} ~idle{time=8, once=true}
  - animation{name=look_around, mode=loop} ~idle{time=9}
```

### Pet Sleep
```yaml
Taming:
  item: minecraft:bone

Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=sit, mode=hold} ~sitting
  - animation{name=sleep, mode=hold} ~idle{time=10}
```
