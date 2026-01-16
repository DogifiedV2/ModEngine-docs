---
sidebar_position: 6
---

# ~health

Fires based on health percentage.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| below | number | 100 | Trigger when health below this % |
| above | number | 0 | Trigger when health above this % |
| once | boolean | false | Only trigger once |

## Examples

```yaml
Skills:
  # Enrage at half health (once)
  - animation{name=enrage} ~health{below=50, once=true}

  # Critical state under 25%
  - animation{name=desperate, mode=loop} ~health{below=25}

  # Between 25% and 50%
  - animation{name=wounded, mode=loop} ~health{below=50, above=25}
```

## Common Patterns

### Simple Enrage
```yaml
Skills:
  - animation{name=enrage} ~health{below=50, once=true}
```

### Multi-Phase Boss
```yaml
Skills:
  # Phase 2 at 66%
  - animation{name=phase2_transform} ~health{below=66, once=true}
  - showbone{bone=phase2_armor} ~health{below=66, once=true}

  # Phase 3 at 33%
  - animation{name=phase3_transform} ~health{below=33, once=true}
  - showbone{bone=phase3_wings} ~health{below=33, once=true}
  - damage{amount=10} @PlayersInRadius{r=10} ~health{below=33, once=true}
```

### Health-Based Abilities
```yaml
Skills:
  # Fire aura when low
  - damage{amount=1, type=fire} @PlayersInRadius{r=4} ~health{below=25}

  # Desperate attack at critical health
  - damage{amount=15, type=explosion} @PlayersInRadius{r=8} ~health{below=10, once=true}
```

### Wounded State
```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle ~health{above=50}
  - animation{name=wounded_idle, mode=loop} ~idle ~health{below=50}
  - animation{name=walk, mode=loop} ~moving ~health{above=50}
  - animation{name=limp, mode=loop} ~moving ~health{below=50}
```
