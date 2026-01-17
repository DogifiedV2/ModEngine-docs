---
sidebar_position: 16
---

# ~onTargetChange

Fires when the entity changes its attack target.

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `once` | `false` | Only trigger once per entity lifetime |

## Context Variables

- `@Target` - The new target entity

## Examples

```yaml
Skills:
  - animation{name=acquire_target} ~onTargetChange
```

## Common Patterns

### Target Acquired
```yaml
Skills:
  - animation{name=lock_on} ~onTargetChange
  - showbone{bone=targeting_laser} ~onTargetChange
```

### Aggro Switch
```yaml
Skills:
  - animation{name=switch_target} ~onTargetChange
```

### Boss Target Call-out
```yaml
Skills:
  - animation{name=point} ~onTargetChange
  - showbone{bone=target_indicator} ~onTargetChange
```

### Hunter Tracking
```yaml
Skills:
  - animation{name=sniff} ~onTargetChange
  - showbone{bone=tracking_particles} ~onTargetChange
```

## Notes

- Only fires when the target changes to a new entity (not when target becomes null)
- Useful for visual feedback when an AI switches between players in multiplayer
