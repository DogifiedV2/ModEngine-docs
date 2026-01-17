---
sidebar_position: 10
---

# ~onAttack

Fires when the entity successfully hits a target with a melee attack.

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `min` | `0` | Minimum damage dealt to trigger |
| `max` | `infinite` | Maximum damage dealt to trigger |
| `once` | `false` | Only trigger once per entity lifetime |

## Context Variables

- `@Target` - The entity that was attacked
- Damage amount available in context

## Examples

```yaml
Skills:
  - animation{name=attack_heavy} ~onAttack
  - damage{amount=5, type=fire} @Target ~onAttack
```

## Common Patterns

### Attack Animation
```yaml
Skills:
  - animation{name=swing} ~onAttack
```

### Lifesteal Effect
```yaml
Skills:
  - animation{name=lifesteal} ~onAttack{min=5}
```

### Heavy Hit Effect
Only trigger on hits dealing 10+ damage:
```yaml
Skills:
  - animation{name=heavy_hit} ~onAttack{min=10}
  - damage{amount=3, type=fire} @Target ~onAttack{min=10}
```

### Boss Attack Pattern
```yaml
Skills:
  - animation{name=slash} ~onAttack
  - showbone{bone=attack_particles} ~onAttack
```
