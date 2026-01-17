---
sidebar_position: 0
---

# Actions

Actions define **what** happens when a skill activates. They are the first component of a skill line and have no prefix.

## Syntax

```
action{params} @target ~trigger
```

The action is required - every skill must do something.

## Quick Example

```yaml
Skills:
  # Play animations
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving

  # Deal damage
  - damage{amount=10, type=explosion} @PlayersInRadius{r=5} ~onDeath

  # Control bone visibility
  - showbone{bone=wings} ~health{below=50, once=true}
  - hidebone{bone=helmet} ~onDeath
```

## All Actions

### Animation

| Action | Description |
|--------|-------------|
| [animation](animation) | Play an animation on the entity |

### Combat

| Action | Description |
|--------|-------------|
| [damage](damage) | Deal damage to targets |

### Visual

| Action | Description |
|--------|-------------|
| [hidebone](hidebone) | Hide a bone on the entity |
| [showbone](showbone) | Show a previously hidden bone |

## Action Parameters

Actions use `{key=value}` syntax for parameters:

```yaml
Skills:
  # Single parameter
  - animation{name=idle}

  # Multiple parameters
  - animation{name=idle, mode=loop, blend=true}

  # Numeric parameters
  - damage{amount=10, type=fire}
```

## Common Patterns

### Basic Animation Set

```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
  - animation{name=hurt} ~onHurt
  - animation{name=death} ~onDeath
```

### Boss Phase Transition

```yaml
Skills:
  - animation{name=enrage, blend=false} ~health{below=50, once=true}
  - showbone{bone=phase2_wings} ~health{below=50, once=true}
  - hidebone{bone=phase1_aura} ~health{below=50, once=true}
  - damage{amount=10, type=magic} @PlayersInRadius{r=10} ~health{below=50, once=true}
```

### Death Effects

```yaml
Skills:
  - animation{name=death} ~onDeath
  - hidebone{bone=helmet} ~onDeath
  - hidebone{bone=weapon} ~onDeath
  - damage{amount=15, type=explosion} @PlayersInRadius{r=8} ~onDeath
```
