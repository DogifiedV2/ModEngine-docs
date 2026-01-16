---
sidebar_position: 2
---

# Damage Types

Damage types used with the `damage` action in Skills.

## Usage

```yaml
Skills:
  - damage{amount=10, type=fire} @PlayersInRadius{r=5} ~onDeath
```

## Available Types

| Type | Description | Visual Effect |
|------|-------------|---------------|
| `generic` | Normal damage | None |
| `fire` | Fire damage | Fire particles, burning |
| `explosion` | Explosion damage | Knockback |
| `magic` | Magic damage | Purple particles |
| `fall` | Fall damage | None |
| `drown` | Drowning damage | Bubble particles |
| `freeze` | Freezing damage | Snow particles |
| `lightning` | Lightning damage | Flash effect |

## Examples

### Fire Aura
```yaml
- damage{amount=2, type=fire} @PlayersInRadius{r=3} ~health{below=50}
```

### Death Explosion
```yaml
- damage{amount=15, type=explosion} @PlayersInRadius{r=8} ~onDeath
```

### Magic Counter-Attack
```yaml
- damage{amount=5, type=magic} @Attacker ~onHurt
```

### Frost Nova
```yaml
- damage{amount=8, type=freeze} @PlayersInRadius{r=6} ~health{below=25, once=true}
```

## Default Type

If no type is specified, `generic` is used:

```yaml
# These are equivalent
- damage{amount=5} @Attacker ~onHurt
- damage{amount=5, type=generic} @Attacker ~onHurt
```
