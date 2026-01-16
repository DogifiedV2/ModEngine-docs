---
sidebar_position: 7
---

# Hidden Bones

Hide specific bones when the entity spawns. Useful for phase changes, equipment, or variants.

## Usage

```yaml
my_entity:
  Model: boss_model
  HiddenBones:
    - wings_extended
    - phase2_armor
    - enraged_aura
```

## Behavior

- Listed bones are hidden when the entity spawns
- Works with both GeckoLib and Blockbench models
- Bone names are case-insensitive
- Use [Skills](skills/overview) to show/hide bones dynamically

## Dynamic Visibility

Combine with `showbone` and `hidebone` actions in Skills:

```yaml
phase_boss:
  Model: boss_model

  HiddenBones:
    - phase2_wings
    - enraged_aura

  Skills:
    # Reveal wings at 50% health
    - showbone{bone=phase2_wings} ~health{below=50, once=true}

    # Show aura at 25% health
    - showbone{bone=enraged_aura} ~health{below=25, once=true}

    # Hide effects on death
    - hidebone{bone=phase2_wings} ~onDeath
    - hidebone{bone=enraged_aura} ~onDeath
```

## Use Cases

### Equipment Variants
```yaml
armored_skeleton:
  Model: skeleton_with_gear
  HiddenBones:
    - helmet
    - shield
  # Show gear based on some condition
```

### Boss Phases
```yaml
three_phase_boss:
  Model: boss
  HiddenBones:
    - phase2_effects
    - phase3_effects
  Skills:
    - showbone{bone=phase2_effects} ~health{below=66, once=true}
    - showbone{bone=phase3_effects} ~health{below=33, once=true}
```

### Folded Wings
```yaml
dragon:
  Model: dragon
  HiddenBones:
    - wings_extended
  Skills:
    # Show extended wings while moving
    - showbone{bone=wings_extended} ~moving
    - hidebone{bone=wings_extended} ~idle
```
