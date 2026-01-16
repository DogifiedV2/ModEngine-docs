---
sidebar_position: 5
---

# ~moving

Fires while the entity is moving.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | number | 0.01 | Minimum speed threshold |

## Examples

```yaml
Skills:
  # Basic walk
  - animation{name=walk, mode=loop} ~moving

  # Run when moving fast
  - animation{name=run, mode=loop} ~moving{speed=0.3}
```

## Common Patterns

### Basic Movement
```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
```

### Speed-Based Animations
```yaml
Skills:
  # Order matters - more specific first
  - animation{name=sprint, mode=loop} ~moving{speed=0.5}
  - animation{name=run, mode=loop} ~moving{speed=0.3}
  - animation{name=walk, mode=loop} ~moving
  - animation{name=idle, mode=loop} ~idle
```

### Flying Entity
```yaml
Skills:
  - animation{name=hover, mode=loop} ~idle
  - animation{name=fly, mode=loop} ~moving
  - animation{name=dive, mode=loop} ~moving{speed=0.5}
```

### Wing Toggle
```yaml
HiddenBones:
  - wings_extended

Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving

  # Show wings when moving fast
  - showbone{bone=wings_extended} ~moving{speed=0.3}
  - hidebone{bone=wings_extended} ~idle
```
