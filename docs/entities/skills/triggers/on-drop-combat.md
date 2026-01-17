---
sidebar_position: 15
---

# ~onDropCombat

Fires when the entity leaves combat (no damage dealt or received for 10 seconds).

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `once` | `false` | Only trigger once per entity lifetime |

## Examples

```yaml
Skills:
  - animation{name=sheathe} ~onDropCombat
  - hidebone{bone=weapon} ~onDropCombat
```

## Common Patterns

### Sheathe Weapon
```yaml
Skills:
  - animation{name=sheathe_weapon} ~onDropCombat
  - hidebone{bone=sword} ~onDropCombat
  - showbone{bone=sheathed_sword} ~onDropCombat
```

### Return to Idle
```yaml
Skills:
  - animation{name=idle} ~onDropCombat
  - hidebone{bone=combat_aura} ~onDropCombat
```

### Calm Down
```yaml
Skills:
  - animation{name=calm} ~onDropCombat
  - hidebone{bone=rage_effects} ~onDropCombat
  - showbone{bone=peaceful_particles} ~onDropCombat
```

### Boss Reset
```yaml
Skills:
  - animation{name=retreat} ~onDropCombat
  - hidebone{bone=phase2_form} ~onDropCombat
  - showbone{bone=normal_form} ~onDropCombat
```

## Notes

- Combat state is tracked using a 200-tick (10 second) window after last damage
- This fires on the transition from "in combat" to "not in combat"
- Useful for resetting visual states when players flee or die
