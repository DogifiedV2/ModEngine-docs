---
sidebar_position: 0
---

# Modules

Modules are configuration sections that define different aspects of your entity. Each module handles a specific feature like AI behavior, stats, or visual settings.

## All Modules

### Core

Essential configuration for every entity.

| Module | Description |
|--------|-------------|
| [Basic Options](basic-options) | Model, Display, Health, Damage, Behavior |
| [Hitbox](hitbox) | Collision box dimensions |
| [Presets](presets) | Pre-configured mob templates |

### AI

Control entity behavior and decision-making.

| Module | Description |
|--------|-------------|
| [AI Goals](ai-goals) | What the entity does (attack, wander, flee) |
| [AI Targets](ai-targets) | What the entity attacks |

### Abilities

Special features and passive properties.

| Module | Description |
|--------|-------------|
| [Traits](traits) | Passive properties (sunburn, climbing, fireimmune) |
| [Taming](taming) | Pet behavior and ownership |
| [Skills](/entities/skills/overview) | Reactive behaviors (animations, damage) |

### Visual

Control entity appearance.

| Module | Description |
|--------|-------------|
| [Hidden Bones](hidden-bones) | Bones hidden at spawn |
| [Equipment](equipment) | Items in equipment slots |

### Loot

Configure what drops on death.

| Module | Description |
|--------|-------------|
| [Drops](drops) | Custom loot drops |

## Using Presets

Presets bundle common configurations together:

```yaml
# Simple - just use a preset
my_skeleton:
  Model: bone_knight
  Preset: skeleton

# Override specific values
tank_zombie:
  Model: armored_zombie
  Preset: zombie
  Health: 100
  Damage: 8
```

See [Presets](presets) for all available presets and customization options.

## Module Order

Modules can be defined in any order. This example shows a recommended organization:

```yaml
my_entity:
  # Identity
  Model: my_model
  Display: '&eMy Entity'
  Preset: zombie

  # Stats
  Health: 50
  Damage: 10

  # Hitbox (if not using preset)
  Hitbox:
    width: 0.6
    height: 2.0

  # AI
  AIGoals:
    - float
    - meleeattack
    - randomstroll
  AITargets:
    - nearestplayer

  # Abilities
  Traits:
    - fireimmune
  Taming:
    item: minecraft:bone

  # Visuals
  HiddenBones:
    - phase2_wings
  Equipment:
    mainhand: minecraft:iron_sword

  # Skills
  Skills:
    - animation{name=idle, mode=loop} ~idle

  # Loot
  Drops:
    - diamond 1 0.1
```
