---
sidebar_position: 7
---

# Pet Triggers

These triggers require the [Taming](/entities/taming) module.

## ~tamed

Fires while the entity is tamed.

```yaml
Skills:
  - animation{name=happy, mode=loop} ~tamed
```

## ~untamed

Fires while the entity is not tamed.

```yaml
Skills:
  - animation{name=wary, mode=loop} ~untamed
```

## ~sitting

Fires while the entity is ordered to sit. Requires `can_sit: true` in Taming config.

```yaml
Skills:
  - animation{name=sit, mode=hold} ~sitting
```

## Examples

### Basic Pet States
```yaml
Taming:
  item: minecraft:bone
  chance: 0.33
  can_sit: true

Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
  - animation{name=sit, mode=hold} ~sitting
  - animation{name=happy, mode=loop} ~tamed
  - animation{name=wary, mode=loop} ~untamed
```

### Pet with Different Idle When Tamed
```yaml
Taming:
  item: minecraft:sweet_berries

Skills:
  - animation{name=walk, mode=loop} ~moving

  # Different idle based on tame status
  - animation{name=friendly_idle, mode=loop} ~idle ~tamed
  - animation{name=cautious_idle, mode=loop} ~idle ~untamed
```

### Pet with Sleep
```yaml
Taming:
  item: minecraft:bone

Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
  - animation{name=sit, mode=hold} ~sitting
  - animation{name=sleep, mode=hold} ~idle{time=10}
  - animation{name=happy_bark} ~tamed
```

### Combat Pet
```yaml
Taming:
  item: minecraft:bone

AIGoals:
  - float
  - meleeattack{speed=1.3}
  - randomstroll
  - lookatplayer

AITargets:
  - hurtbytarget

Skills:
  - animation{name=idle, mode=loop} ~idle
  - animation{name=walk, mode=loop} ~moving
  - animation{name=sit, mode=hold} ~sitting
  - animation{name=attack} ~onHurt
  - animation{name=howl} ~tamed
```
