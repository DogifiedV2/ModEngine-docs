---
sidebar_position: 1
---

# @Self

Targets the entity itself. This is the default target if none is specified.

## Parameters

None.

## Examples

```yaml
Skills:
  # These are equivalent
  - animation{name=hurt} @Self ~onHurt
  - animation{name=hurt} ~onHurt
```

## Usage

`@Self` is implicit - you rarely need to write it explicitly. It's mainly useful for clarity when you have multiple skills with different targets:

```yaml
Skills:
  # Self animations
  - animation{name=hurt} @Self ~onHurt
  - animation{name=enrage} @Self ~health{below=50, once=true}

  # Damage to others
  - damage{amount=5} @Attacker ~onHurt
  - damage{amount=10} @PlayersInRadius{r=8} ~onDeath
```
