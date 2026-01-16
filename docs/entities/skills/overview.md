---
sidebar_position: 1
---

# Skills Overview

The Skills system lets you define reactive behaviors using a simple action-target-trigger syntax.

## Syntax

```
action{params} @target{params} ~trigger{params}
```

| Component | Prefix | Required | Description |
|-----------|--------|----------|-------------|
| Action | (none) | Yes | What to do |
| Target | `@` | No | Who it affects (default: @Self) |
| Trigger | `~` | Yes | When it happens |

## Quick Example

```yaml
Skills:
  # Play idle animation while idle
  - animation{name=idle, mode=loop} ~idle

  # Play walk animation while moving
  - animation{name=walk, mode=loop} ~moving

  # Deal explosion damage to nearby players on death
  - damage{amount=10, type=explosion} @PlayersInRadius{r=5} ~onDeath
```

## Components

### Actions
What happens when the skill activates.

| Action | Description |
|--------|-------------|
| [animation](actions#animation) | Play an animation |
| [damage](actions#damage) | Deal damage |
| [hidebone](actions#hidebone) | Hide a bone |
| [showbone](actions#showbone) | Show a bone |

### Targets
Who the action affects.

| Target | Description |
|--------|-------------|
| [@Self](targets#self) | The entity itself (default) |
| [@Attacker](targets#attacker) | Entity that last attacked |
| [@PlayersInRadius](targets#playersinradius) | Players within range |

### Triggers
When the skill activates.

**Event triggers** (fire once per event):
| Trigger | Description |
|---------|-------------|
| [~onSpawn](triggers#onspawn) | When spawned |
| [~onDeath](triggers#ondeath) | When killed |
| [~onHurt](triggers#onhurt) | When damaged |

**State triggers** (active while condition is true):
| Trigger | Description |
|---------|-------------|
| [~idle](triggers#idle) | While not moving |
| [~moving](triggers#moving) | While moving |
| [~health](triggers#health) | Based on health % |

**Pet triggers** (require [Taming](../taming)):
| Trigger | Description |
|---------|-------------|
| [~tamed](triggers#tamed) | While tamed |
| [~untamed](triggers#untamed) | While not tamed |
| [~sitting](triggers#sitting) | While sitting |

## Skill Order

Skills are evaluated in order. For state triggers (like `~idle` and `~moving`), the first matching animation wins.

```yaml
Skills:
  # These are mutually exclusive - order matters
  - animation{name=run, mode=loop} ~moving{speed=0.3}   # Fast movement
  - animation{name=walk, mode=loop} ~moving             # Normal movement
  - animation{name=idle, mode=loop} ~idle               # Standing still
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

### Boss with Phases
```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
  - animation{name=enrage} ~health{below=50, once=true}
  - showbone{bone=phase2_effects} ~health{below=50, once=true}
  - damage{amount=15, type=fire} @PlayersInRadius{r=8} ~onDeath
```

### Counter-Attack
```yaml
Skills:
  - damage{amount=3, type=magic} @Attacker ~onHurt
```
