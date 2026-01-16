---
sidebar_position: 3
---

# Targets

Targets specify who is affected by an action. If no target is specified, `@Self` is used.

## @Self

Targets the entity itself. This is the default.

```yaml
Skills:
  # These are equivalent
  - animation{name=hurt} @Self ~onHurt
  - animation{name=hurt} ~onHurt
```

## @Attacker

Targets the entity that last attacked this entity.

```yaml
Skills:
  # Reflect damage to attacker
  - damage{amount=3, type=magic} @Attacker ~onHurt

  # Counter-attack with fire
  - damage{amount=5, type=fire} @Attacker ~onHurt{min=10}
```

:::note
`@Attacker` only works with triggers that involve being attacked, like `~onHurt`. It has no effect with triggers like `~onSpawn` or `~idle`.
:::

## @PlayersInRadius

Targets players (or other entities) within a radius.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| r | number | 32.0 | Radius in blocks |
| filter | string | players | Entity filter |

**Filters:**
- `players` - Only players (default)
- `living` - All living entities
- `all` - All entities

```yaml
Skills:
  # Damage nearby players on death
  - damage{amount=10, type=explosion} @PlayersInRadius{r=5} ~onDeath

  # Large radius magic damage
  - damage{amount=5, type=magic} @PlayersInRadius{r=16} ~health{below=25, once=true}

  # Affect all living entities
  - damage{amount=3, type=fire} @PlayersInRadius{r=8, filter=living} ~onDeath
```

## Target Examples

### Death Explosion
```yaml
Skills:
  - damage{amount=15, type=explosion} @PlayersInRadius{r=8} ~onDeath
  - animation{name=death_explosion} ~onDeath
```

### Thorns Effect
```yaml
Skills:
  - damage{amount=2} @Attacker ~onHurt
```

### Enrage Aura
```yaml
Skills:
  # Constant damage aura when low health
  - damage{amount=1, type=fire} @PlayersInRadius{r=4} ~health{below=25}
```

### Multi-Target Boss
```yaml
boss_entity:
  Model: boss
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving

    # Self animations
    - animation{name=hurt} ~onHurt
    - animation{name=enrage} ~health{below=50, once=true}

    # Attack nearby players
    - damage{amount=8, type=magic} @PlayersInRadius{r=10} ~health{below=50, once=true}

    # Death explosion
    - damage{amount=20, type=explosion} @PlayersInRadius{r=12} ~onDeath
```
