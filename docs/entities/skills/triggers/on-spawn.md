---
sidebar_position: 1
---

# ~onSpawn

Fires once when the entity spawns into the world.

## Parameters

None.

## Examples

```yaml
Skills:
  - animation{name=spawn} ~onSpawn
  - animation{name=appear, blend=false} ~onSpawn
```

## Common Patterns

### Spawn Animation
```yaml
Skills:
  - animation{name=spawn} ~onSpawn
  - animation{name=idle, mode=loop} ~idle
```

### Boss Entrance
```yaml
Skills:
  - animation{name=dramatic_entrance, blend=false} ~onSpawn
  - damage{amount=5, type=explosion} @PlayersInRadius{r=6} ~onSpawn
```
