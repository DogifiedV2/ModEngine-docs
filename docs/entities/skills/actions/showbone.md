---
sidebar_position: 4
---

# showbone

Shows a previously hidden bone. Works with both GeckoLib and Blockbench models.

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| bone | string | required | Bone name to show |

## Notes

- Bone names are case-insensitive
- Typically used with bones hidden via [HiddenBones](/entities/modules/hidden-bones) module
- Use [hidebone](hidebone) to hide bones dynamically

## Examples

```yaml
Skills:
  # Reveal wings at low health
  - showbone{bone=wings_extended} ~health{below=50, once=true}

  # Show enraged effects
  - showbone{bone=fire_aura} ~health{below=25, once=true}

  # Show extended wings while moving
  - showbone{bone=wings_extended} ~moving
```

## Common Patterns

### Boss Phase Reveals
```yaml
HiddenBones:
  - phase2_wings
  - phase2_crown
  - enraged_aura

Skills:
  # Phase 2 at 50% health
  - showbone{bone=phase2_wings} ~health{below=50, once=true}
  - showbone{bone=phase2_crown} ~health{below=50, once=true}

  # Enrage at 25% health
  - showbone{bone=enraged_aura} ~health{below=25, once=true}
```

### Conditional Equipment
```yaml
HiddenBones:
  - battle_armor

Skills:
  # Show armor when in combat (low health = been attacked)
  - showbone{bone=battle_armor} ~health{below=100, once=true}
```

### State-Based Visibility
```yaml
HiddenBones:
  - sleeping_zzz

Skills:
  - showbone{bone=sleeping_zzz} ~idle{time=10}
  - hidebone{bone=sleeping_zzz} ~moving
```
