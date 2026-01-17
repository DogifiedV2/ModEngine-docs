---
sidebar_position: 1
---

# Entity Overview

Entities are defined using YAML configuration files placed in `config/modengine/entities/`.

## File Structure

Each YAML file can contain multiple entity definitions:

```yaml
# config/modengine/entities/my_mobs.yml

zombie_variant:
  Model: zombie_model
  Display: '&cZombie Variant'
  Health: 30
  Behavior: HOSTILE

friendly_creature:
  Model: creature_model
  Display: '&aFriendly Creature'
  Health: 20
  Behavior: PASSIVE
```

## Configuration Sections

| Section                                   | Required | Description |
|-------------------------------------------|----------|-------------|
| [Model](modules/basic-options#model)      | Yes | The model to use for this entity |
| [Display](modules/basic-options#display)  | No | Custom display name |
| [Health](modules/basic-options#health)    | No | Maximum health points |
| [Damage](modules/basic-options#damage)    | No | Base attack damage |
| [Style](modules/basic-options#AnimationStyle)      | No | Procedural animation style |
| [Behavior](modules/basic-options#behavior) | No | AI behavior preset |
| [Hitbox](modules/hitbox)                  | No | Custom hitbox dimensions |
| [AIGoals](modules/ai-goals)               | No | Custom AI goals |
| [AITargets](modules/ai-targets)           | No | Custom targeting behavior |
| [Taming](modules/taming)                  | No | Pet/taming behavior |
| [HiddenBones](modules/hidden-bones)       | No | Bones hidden by default |
| [Drops](modules/drops)                    | No | Custom death loot drops |
| [Skills](skills/overview)                 | No | Reactive behaviors |

## Model Loading

Models are loaded from `config/modengine/entities/models/`:

**Blockbench (.bbmodel):**
```
models/my_model.bbmodel
```

**GeckoLib (folder):**
```
models/my_model/
├── model.geo.json      # Required
├── model.animation.json # Optional
└── default.png          # Texture(s)
```

The model ID is the filename (without extension) or folder name, in lowercase.

## Commands

| Command | Description |
|---------|-------------|
| `/mm spawn <id>` | Spawn an entity |
| `/mm list` | List all loaded entities |
| `/mm reload` | Reload all configs |
| `/mm select` | Select entity you're looking at |
| `/mm debug` | Toggle debug overlay |
| `/mm playanimation <name>` | Play animation on selected entity |
