---
sidebar_position: 3
---

# @PlayersInRadius

Targets players (or other entities) within a radius around the entity.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| r | number | 32.0 | Radius in blocks |
| filter | string | players | Entity filter |

## Filters

| Filter | Description |
|--------|-------------|
| `players` | Only players (default) |
| `living` | All living entities (players, mobs, animals) |
| `all` | All entities including non-living |

## Examples

```yaml
Skills:
  # Damage nearby players on death
  - damage{amount=10, type=explosion} @PlayersInRadius{r=5} ~onDeath

  # Large radius magic damage
  - damage{amount=5, type=magic} @PlayersInRadius{r=16} ~health{below=25, once=true}

  # Affect all living entities
  - damage{amount=3, type=fire} @PlayersInRadius{r=8, filter=living} ~onDeath
```

## Common Patterns

### Death Explosion
```yaml
Skills:
  - damage{amount=15, type=explosion} @PlayersInRadius{r=8} ~onDeath
  - animation{name=death_explosion} ~onDeath
```

### Enrage AOE
```yaml
Skills:
  # Burst damage when entering enrage
  - damage{amount=10, type=magic} @PlayersInRadius{r=12} ~health{below=50, once=true}
  - animation{name=enrage} ~health{below=50, once=true}
```

### Constant Aura
```yaml
Skills:
  # Fire aura while low health
  - damage{amount=1, type=fire} @PlayersInRadius{r=4} ~health{below=25}
```

### Multi-Range Attack
```yaml
Skills:
  # Close range = high damage
  - damage{amount=10, type=explosion} @PlayersInRadius{r=4} ~onDeath

  # Far range = low damage
  - damage{amount=3, type=magic} @PlayersInRadius{r=12} ~onDeath
```
