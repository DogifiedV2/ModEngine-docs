---
sidebar_position: 2
---

# damage

Deals damage to targets.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| amount | number | 1.0 | Damage amount |
| type | string | generic | Damage type |

## Damage Types

| Type | Description |
|------|-------------|
| `generic` | Normal damage |
| `fire` | Fire damage |
| `explosion` | Explosion damage (knockback) |
| `magic` | Magic damage |
| `fall` | Fall damage |
| `drown` | Drowning damage |
| `freeze` | Freezing damage |
| `lightning` | Lightning damage |

See [damage types reference](/reference/damage-types) for more details.

## Examples

```yaml
Skills:
  # Explosion on death
  - damage{amount=10, type=explosion} @PlayersInRadius{r=5} ~onDeath

  # Fire aura at low health
  - damage{amount=2, type=fire} @PlayersInRadius{r=3} ~health{below=25}

  # Reflect damage to attacker
  - damage{amount=3, type=magic} @Attacker ~onHurt
```

## Common Patterns

### Death Explosion
```yaml
Skills:
  - damage{amount=15, type=explosion} @PlayersInRadius{r=8} ~onDeath
```

### Thorns Effect
```yaml
Skills:
  - damage{amount=2} @Attacker ~onHurt
```

### Enrage Aura
```yaml
Skills:
  # Constant fire damage when low health
  - damage{amount=1, type=fire} @PlayersInRadius{r=4} ~health{below=25}
```

### Phase Transition Attack
```yaml
Skills:
  - damage{amount=10, type=magic} @PlayersInRadius{r=10} ~health{below=50, once=true}
```
