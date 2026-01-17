---
sidebar_position: 11
---

# ~onTimer

Fires repeatedly at a specified interval. Essential for periodic abilities like auras, buffs, and spawning adds.

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `interval` | `20` | Ticks between executions (20 ticks = 1 second) |

## Examples

```yaml
Skills:
  - animation{name=pulse} ~onTimer{interval=40}
  - damage{amount=2, type=fire} @PlayersInRadius{r=5} ~onTimer{interval=60}
```

## Common Patterns

### Fire Aura (Every 2 seconds)
```yaml
Skills:
  - damage{amount=1, type=fire} @PlayersInRadius{r=3} ~onTimer{interval=40}
```

### Healing Pulse (Every 3 seconds)
```yaml
Skills:
  - animation{name=heal_pulse} ~onTimer{interval=60}
```

### Fast Attack Animation (Every 0.5 seconds)
```yaml
Skills:
  - animation{name=idle_combat} ~onTimer{interval=10}
```

### Boss Phase Timer
```yaml
Skills:
  - animation{name=charge_attack} ~onTimer{interval=100}
  - damage{amount=15, type=magic} @PlayersInRadius{r=8} ~onTimer{interval=100}
```

### Ambient Effects
```yaml
Skills:
  - showbone{bone=sparkles} ~onTimer{interval=20}
  - hidebone{bone=sparkles} ~onTimer{interval=30}
```

## Notes

- Timer starts when the entity spawns
- Each timer skill tracks its own interval independently
- Very short intervals (< 5 ticks) may impact performance with many entities
