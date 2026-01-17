---
sidebar_position: 3
---

# hidebone

Hides a bone on the entity. Works with both GeckoLib and Blockbench models.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| bone | string | required | Bone name to hide |

## Notes

- Bone names are case-insensitive
- Hidden bones are not rendered but still exist in the hierarchy
- Use [showbone](showbone) to reveal hidden bones
- For bones hidden at spawn, use the [HiddenBones](/entities/modules/hidden-bones) module instead

## Examples

```yaml
Skills:
  # Hide helmet on death
  - hidebone{bone=helmet} ~onDeath

  # Hide folded wings when moving
  - hidebone{bone=wings_folded} ~moving

  # Hide phase 1 effects when entering phase 2
  - hidebone{bone=phase1_aura} ~health{below=50, once=true}
```

## Common Patterns

### Equipment Loss on Death
```yaml
Skills:
  - hidebone{bone=helmet} ~onDeath
  - hidebone{bone=weapon} ~onDeath
  - hidebone{bone=shield} ~onDeath
```

### Wing State Toggle
```yaml
HiddenBones:
  - wings_extended

Skills:
  # Show extended wings while moving, hide folded
  - showbone{bone=wings_extended} ~moving
  - hidebone{bone=wings_folded} ~moving

  # Reverse when idle
  - hidebone{bone=wings_extended} ~idle
  - showbone{bone=wings_folded} ~idle
```

### Phase Transition
```yaml
Skills:
  - hidebone{bone=phase1_crown} ~health{below=50, once=true}
  - showbone{bone=phase2_crown} ~health{below=50, once=true}
```
