---
sidebar_position: 3
---

# ~onHurt

Fires when the entity takes damage.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| min | number | 0 | Minimum damage to trigger |
| max | number | infinity | Maximum damage to trigger |
| once | boolean | false | Only trigger once ever |

## Examples

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

## Common Patterns

### Basic Hurt Animation
```yaml
Skills:
  - animation{name=hurt} ~onHurt
```

### Damage-Based Reactions
```yaml
Skills:
  - animation{name=flinch} ~onHurt{max=5}
  - animation{name=hurt} ~onHurt{min=5, max=15}
  - animation{name=stagger, blend=false} ~onHurt{min=15}
```

### Counter-Attack
```yaml
Skills:
  - animation{name=hurt} ~onHurt
  - damage{amount=3, type=magic} @Attacker ~onHurt
```

### First Blood
```yaml
Skills:
  - animation{name=enrage} ~onHurt{once=true}
  - damage{amount=5} @PlayersInRadius{r=8} ~onHurt{once=true}
```
