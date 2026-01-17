---
sidebar_position: 0
---

# Targets

Targets define **who** a skill affects. They are prefixed with `@` and come between the action and trigger.

## Syntax

```
action{params} @target{params} ~trigger
```

If no target is specified, `@Self` is used by default.

## Quick Example

```yaml
Skills:
  # Target self (default)
  - animation{name=hurt} ~onHurt

  # Target the attacker
  - damage{amount=3} @Attacker ~onHurt

  # Target nearby players
  - damage{amount=10, type=explosion} @PlayersInRadius{r=5} ~onDeath
```

## All Targets

| Target | Description |
|--------|-------------|
| [@Self](self) | The entity itself (default) |
| [@Attacker](attacker) | Entity that last attacked |
| [@PlayersInRadius](players-in-radius) | Players within a radius |

## Target Context

Different triggers provide different target contexts:

| Trigger | Available Targets |
|---------|-------------------|
| `~onHurt` | `@Self`, `@Attacker` |
| `~onAttack`, `~onKill` | `@Self`, `@Target` |
| `~onDeath`, `~onSpawn` | `@Self`, `@PlayersInRadius` |
| `~onInteract` | `@Self`, `@TriggerSource` |
| `~idle`, `~moving` | `@Self`, `@PlayersInRadius` |

## Common Patterns

### Counter-Attack

```yaml
Skills:
  - damage{amount=3, type=magic} @Attacker ~onHurt
```

### Death Explosion

```yaml
Skills:
  - damage{amount=15, type=explosion} @PlayersInRadius{r=8} ~onDeath
```

### Scaling Retaliation

```yaml
Skills:
  # Small hits = small retaliation
  - damage{amount=1} @Attacker ~onHurt{max=5}

  # Big hits = big retaliation
  - damage{amount=5, type=fire} @Attacker ~onHurt{min=10}
```
