---
sidebar_position: 2
---

# ~onDeath

Fires once when the entity dies.

## Parameters

None.

## Examples

```yaml
Skills:
  - animation{name=death} ~onDeath
  - damage{amount=10, type=explosion} @PlayersInRadius{r=5} ~onDeath
```

## Common Patterns

### Death Animation
```yaml
Skills:
  - animation{name=death} ~onDeath
```

### Death Explosion
```yaml
Skills:
  - animation{name=death_explosion} ~onDeath
  - damage{amount=15, type=explosion} @PlayersInRadius{r=8} ~onDeath
```

### Drop Effects
```yaml
Skills:
  - hidebone{bone=helmet} ~onDeath
  - hidebone{bone=weapon} ~onDeath
  - showbone{bone=death_particles} ~onDeath
```

### Boss Death Sequence
```yaml
Skills:
  - animation{name=death_dramatic} ~onDeath
  - hidebone{bone=enraged_aura} ~onDeath
  - hidebone{bone=phase2_wings} ~onDeath
  - damage{amount=20, type=explosion} @PlayersInRadius{r=12} ~onDeath
```
