---
sidebar_position: 1
---

# animation

Plays an animation on the entity.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| name | string | required | Animation name from the model |
| mode | string | once | `once`, `loop`, or `hold` |
| blend | boolean | true | Blend from previous animation |

## Modes

- `once` - Play once then stop
- `loop` - Repeat continuously
- `hold` - Play once and hold the last frame

## Examples

```yaml
Skills:
  # Loop while idle
  - animation{name=idle, mode=loop} ~idle

  # Play once when hurt
  - animation{name=hurt} ~onHurt

  # Hold pose while sitting
  - animation{name=sit, mode=hold} ~sitting

  # No blending for instant switch
  - animation{name=transform, blend=false} ~health{below=50, once=true}
```

## Common Patterns

### Basic Animation Set
```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
  - animation{name=hurt} ~onHurt
  - animation{name=death} ~onDeath
```

### Speed-Based Animations
```yaml
Skills:
  - animation{name=run, mode=loop} ~moving{speed=0.3}
  - animation{name=walk, mode=loop} ~moving
  - animation{name=idle, mode=loop} ~idle
```

### Phase Transitions
```yaml
Skills:
  - animation{name=enrage, blend=false} ~health{below=50, once=true}
  - animation{name=transform} ~health{below=25, once=true}
```
