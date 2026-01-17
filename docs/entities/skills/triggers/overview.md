---
sidebar_position: 0
---

# Triggers

Triggers define **when** a skill activates. They are always prefixed with `~` and come at the end of a skill line.

## Syntax

```
action{params} @target{params} ~trigger{params}
```

A skill line always ends with at least one trigger. Multiple triggers can be combined on a single line.

## Quick Example

```yaml
Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
  - animation{name=hurt} ~onHurt
  - animation{name=death} ~onDeath
```

## All Triggers

### Lifecycle

Triggers that fire during entity lifecycle events.

| Trigger | Description |
|---------|-------------|
| [~onSpawn](on-spawn) | Fires once when the entity spawns into the world |
| [~onDeath](on-death) | Fires once when the entity dies |
| [~onLoad](on-load) | Fires when an entity is loaded from save data |
| [~onDespawn](on-despawn) | Fires when an entity is removed (not death) |

### Combat

Triggers related to combat actions and state.

| Trigger | Description |
|---------|-------------|
| [~onHurt](on-hurt) | Fires when the entity takes damage |
| [~onAttack](on-attack) | Fires when the entity hits a target with a melee attack |
| [~onKill](on-kill) | Fires when the entity kills another entity |
| [~onEnterCombat](on-enter-combat) | Fires when the entity first enters combat |
| [~onDropCombat](on-drop-combat) | Fires when the entity leaves combat (10s no damage) |
| [~onTargetChange](on-target-change) | Fires when the entity changes its attack target |
| [~onShoot](on-shoot) | Fires when the entity performs a ranged attack |
| [~onExplode](on-explode) | Fires just before a creeper-like entity explodes |

### Utility

General purpose triggers for timers, interaction, and signals.

| Trigger | Description |
|---------|-------------|
| [~onTimer](on-timer) | Fires repeatedly at a specified interval |
| [~onInteract](on-interact) | Fires when a player right-clicks the entity |
| [~onSignal](on-signal) | Fires when the entity receives a signal |

### State

Continuous triggers that fire while a condition is true.

| Trigger | Description |
|---------|-------------|
| [~idle](idle) | Fires while the entity is not moving |
| [~moving](moving) | Fires while the entity is moving |
| [~health](health) | Fires based on health percentage thresholds |

### Pet

Triggers for tameable entities. Require the [Taming](/entities/modules/taming) module.

| Trigger | Description |
|---------|-------------|
| [~tamed](pet-triggers#tamed) | Fires while the entity is tamed |
| [~untamed](pet-triggers#untamed) | Fires while the entity is not tamed |
| [~sitting](pet-triggers#sitting) | Fires while the entity is ordered to sit |

## Common Parameters

Most triggers support these common parameters:

| Parameter | Type | Description |
|-----------|------|-------------|
| `once` | boolean | Only trigger once per entity lifetime |

Some triggers have additional parameters documented on their individual pages.

## Combining Triggers

You can combine state triggers on a single line:

```yaml
Skills:
  # Different idle animations based on tame status
  - animation{name=happy_idle, mode=loop} ~idle ~tamed
  - animation{name=wary_idle, mode=loop} ~idle ~untamed

  # Different movement at low health
  - animation{name=limp, mode=loop} ~moving ~health{below=25}
  - animation{name=walk, mode=loop} ~moving
```

## Skill Order

Skills are evaluated in order. For state triggers, the **first matching** skill wins:

```yaml
Skills:
  # More specific conditions first
  - animation{name=sprint, mode=loop} ~moving{speed=0.5}
  - animation{name=run, mode=loop} ~moving{speed=0.3}
  - animation{name=walk, mode=loop} ~moving
  - animation{name=idle, mode=loop} ~idle
```
