---
sidebar_position: 1
---

# Basic Mob

A simple hostile mob with animations.

## Config

```yaml
# config/modengine/entities/zombie_variant.yml

zombie_variant:
  Model: zombie_variant
  Display: '&cZombie Variant'
  Health: 30
  Damage: 6
  AnimationStyle: Zombie
  Behavior: HOSTILE
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
    - animation{name=hurt} ~onHurt
    - animation{name=death} ~onDeath
```

## Breakdown

| Option | Value | Purpose |
|--------|-------|---------|
| Model | zombie_variant | Model file in models folder |
| Display | &cZombie Variant | Red colored name |
| Health | 30 | 15 hearts |
| Damage | 6 | 3 hearts per hit |
| AnimationStyle | Zombie | Humanoid procedural animation |
| Behavior | HOSTILE | Attacks players on sight |

## Model Requirements

For the `Zombie` style, your model needs these bones:
- `head`
- `body`
- `left_arm`
- `right_arm`
- `left_leg`
- `right_leg`

## Variations

### Passive Version
```yaml
friendly_creature:
  Model: creature
  Display: '&aFriendly Creature'
  Health: 20
  Behavior: PASSIVE
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
```

### Neutral Version
```yaml
neutral_golem:
  Model: golem
  Display: '&7Stone Golem'
  Health: 50
  Damage: 10
  Behavior: NEUTRAL
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
    - animation{name=hurt} ~onHurt
```

### Custom AI Version
```yaml
custom_zombie:
  Model: zombie_variant
  Display: '&cSmart Zombie'
  Health: 40
  Damage: 8
  AIGoals:
    - float
    - meleeattack{speed=1.3, alwaysfollow=true}
    - randomstroll{speed=0.6}
    - lookatplayer{range=16}
  AITargets:
    - nearestplayer
    - hurtbytarget{alertallies=true}
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
```
