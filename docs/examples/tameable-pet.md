---
sidebar_position: 3
---

# Tameable Pet

A pet that can be tamed, follows its owner, and sits on command.

## Config

```yaml
# config/modengine/entities/pets.yml

pet_fox:
  Model: custom_fox
  Display: '&6Tameable Fox'
  Health: 20
  AnimationStyle: Quadruped

  Taming:
    item: minecraft:sweet_berries
    chance: 0.25
    follow_distance: 12.0
    stop_distance: 2.0
    teleport_distance: 15.0
    can_sit: true
    follow_speed: 1.2

  Skills:
    # Basic movement
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
    - animation{name=run, mode=loop} ~moving{speed=0.3}

    # Sitting
    - animation{name=sit, mode=hold} ~sitting

    # Tamed vs untamed behavior
    - animation{name=happy_idle, mode=loop} ~tamed
    - animation{name=wary, mode=loop} ~untamed

    # Sleep after idle for a while
    - animation{name=sleep, mode=hold} ~idle{time=10}
```

## Behavior Explanation

### Taming
- Use sweet berries on the fox
- 25% chance of success per berry
- Hearts appear on success

### Following
- Starts following when 12 blocks away
- Stops when within 2 blocks
- Teleports if owner goes beyond 15 blocks

### Sitting
- Right-click tamed fox to toggle sitting
- While sitting, stays in place
- Shows sit animation

### Animations
- Different idle when tamed vs untamed
- Falls asleep after 10 seconds of idle
- Runs when moving fast, walks when slow

## Model Requirements

For `Quadruped` style:
- `head`
- `body`
- `left_front_leg`
- `right_front_leg`
- `left_hind_leg`
- `right_hind_leg`

## Variations

### Simple Pet
```yaml
simple_pet:
  Model: pet_model
  Display: '&ePet'
  Taming:
    item: minecraft:bone
    chance: 0.33
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
    - animation{name=sit, mode=hold} ~sitting
```

### Rare Pet
```yaml
dragon_pet:
  Model: baby_dragon
  Display: '&5&lBaby Dragon'
  Health: 40

  Taming:
    item: minecraft:dragon_breath
    chance: 0.05
    follow_speed: 1.5
    teleport_distance: 25.0

  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=fly, mode=loop} ~moving
    - animation{name=perch, mode=hold} ~sitting
    - animation{name=roar} ~onHurt
```

### Combat Pet
```yaml
combat_wolf:
  Model: dire_wolf
  Display: '&7Dire Wolf'
  Health: 30
  Damage: 6

  Taming:
    item: minecraft:bone
    chance: 0.2

  AIGoals:
    - float
    - meleeattack{speed=1.4}
    - randomstroll
    - lookatplayer

  AITargets:
    - hurtbytarget{alertallies=true}

  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
    - animation{name=sit, mode=hold} ~sitting
    - animation{name=attack} ~onHurt
    - animation{name=howl} ~tamed
```
