---
sidebar_position: 2
---

# Boss with Phases

A boss entity with multiple phases, bone visibility changes, and special attacks.

## Config

```yaml
# config/modengine/entities/fire_boss.yml

fire_elemental:
  Model: fire_elemental
  Display: '&c&lFire Elemental'
  Health: 200
  Damage: 12

  Hitbox:
    width: 1.5
    height: 3.0
    eye_height: 2.5

  AIGoals:
    - float
    - meleeattack{speed=1.2}
    - randomstroll{speed=0.5}
    - lookatplayer{range=20}

  AITargets:
    - nearestplayer

  HiddenBones:
    - phase2_wings
    - phase2_crown
    - enraged_aura
    - death_particles

  Skills:
    # Basic animations
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
    - animation{name=spawn} ~onSpawn
    - animation{name=hurt} ~onHurt

    # Phase 2 at 50% health
    - animation{name=transform_phase2} ~health{below=50, once=true}
    - showbone{bone=phase2_wings} ~health{below=50, once=true}
    - showbone{bone=phase2_crown} ~health{below=50, once=true}
    - damage{amount=8, type=fire} @PlayersInRadius{r=10} ~health{below=50, once=true}

    # Enrage at 25% health
    - animation{name=enrage} ~health{below=25, once=true}
    - showbone{bone=enraged_aura} ~health{below=25, once=true}
    - damage{amount=12, type=fire} @PlayersInRadius{r=12} ~health{below=25, once=true}

    # Death sequence
    - animation{name=death} ~onDeath
    - showbone{bone=death_particles} ~onDeath
    - damage{amount=20, type=explosion} @PlayersInRadius{r=15} ~onDeath
```

## Phase Breakdown

### Phase 1 (100% - 51% Health)
- Normal appearance
- Standard attacks
- Basic idle/walk animations

### Phase 2 (50% - 26% Health)
- Wings and crown appear
- Transformation animation plays
- Fire burst damages nearby players

### Phase 3 / Enrage (25% - 0% Health)
- Enraged aura appears
- Enrage animation plays
- Another fire burst

### Death
- Death animation plays
- Death particles appear
- Massive explosion damages players

## Model Setup

Your model needs these bones:
- Standard animation bones (depends on Style, or custom)
- `phase2_wings` - Hidden initially, shown at 50%
- `phase2_crown` - Hidden initially, shown at 50%
- `enraged_aura` - Hidden initially, shown at 25%
- `death_particles` - Hidden initially, shown on death

## Simpler Version

A boss without bone visibility:

```yaml
simple_boss:
  Model: boss
  Display: '&5&lDark Lord'
  Health: 150
  Damage: 10
  Behavior: HOSTILE

  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving

    # Phase transitions (animation only)
    - animation{name=power_up} ~health{below=50, once=true}
    - animation{name=enrage} ~health{below=25, once=true}

    # Special attacks
    - damage{amount=6, type=magic} @PlayersInRadius{r=8} ~health{below=50, once=true}
    - damage{amount=15, type=explosion} @PlayersInRadius{r=10} ~onDeath
```
