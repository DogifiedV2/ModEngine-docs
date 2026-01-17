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
| [animation](actions/animation) | Play an animation |
| [damage](actions/damage) | Deal damage |
| [hidebone](actions/hidebone) | Hide a bone |
| [showbone](actions/showbone) | Show a bone |

### Targets
Who the action affects.

| Target | Description |
|--------|-------------|
| [@Self](targets/self) | The entity itself (default) |
| [@Attacker](targets/attacker) | Entity that last attacked |
| [@PlayersInRadius](targets/players-in-radius) | Players within range |

### Triggers
When the skill activates.

**Lifecycle triggers**:

| Trigger | Description |
|---------|-------------|
| [~onSpawn](triggers/on-spawn) | When entity spawns |
| [~onDeath](triggers/on-death) | When entity dies |
| [~onLoad](triggers/on-load) | When entity loads from save |
| [~onDespawn](triggers/on-despawn) | When entity is removed (not death) |

**Combat triggers**:

| Trigger | Description |
|---------|-------------|
| [~onHurt](triggers/on-hurt) | When entity takes damage |
| [~onAttack](triggers/on-attack) | When entity attacks |
| [~onKill](triggers/on-kill) | When entity kills something |
| [~onEnterCombat](triggers/on-enter-combat) | When entering combat |
| [~onDropCombat](triggers/on-drop-combat) | When leaving combat |
| [~onTargetChange](triggers/on-target-change) | When target changes |
| [~onShoot](triggers/on-shoot) | When firing ranged attack |
| [~onExplode](triggers/on-explode) | When exploding (creeper-like) |

**Utility triggers**:

| Trigger | Description |
|---------|-------------|
| [~onTimer](triggers/on-timer) | Periodic execution |
| [~onInteract](triggers/on-interact) | When player right-clicks |
| [~onSignal](triggers/on-signal) | When receiving a signal |

**State triggers** (active while condition is true):

| Trigger | Description |
|---------|-------------|
| [~idle](triggers/idle) | While not moving |
| [~moving](triggers/moving) | While moving |
| [~health](triggers/health) | Based on health % |

**Pet triggers** (require [Taming](../modules/taming)):

| Trigger | Description |
|---------|-------------|
| [~tamed / ~untamed / ~sitting](triggers/pet-triggers) | Pet state triggers |

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
