---
sidebar_position: 13
---

# ~onKill

Fires when the entity kills another entity.

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `once` | `false` | Only trigger once per entity lifetime |
| `playeronly` | `false` | Only trigger when killing players |

## Context Variables

- `@Target` - The entity that was killed

## Examples

```yaml
Skills:
  - animation{name=victory} ~onKill
  - animation{name=consume} ~onKill{playeronly=true}
```

## Common Patterns

### Victory Animation
```yaml
Skills:
  - animation{name=roar} ~onKill
```

### Player Kill Celebration
```yaml
Skills:
  - animation{name=taunt} ~onKill{playeronly=true}
  - showbone{bone=trophy} ~onKill{playeronly=true}
```

### Consume Effect
```yaml
Skills:
  - animation{name=eat} ~onKill
  - hidebone{bone=hungry_indicator} ~onKill
```

### Berserker Power-Up
```yaml
Skills:
  - animation{name=power_up} ~onKill
  - showbone{bone=blood_aura} ~onKill
```

## Notes

- This triggers after the killing blow is dealt
- Works with both melee attacks (doHurtTarget) and ranged attacks if they cause death
