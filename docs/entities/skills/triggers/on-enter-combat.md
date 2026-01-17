---
sidebar_position: 14
---

# ~onEnterCombat

Fires when the entity first enters combat (gets attacked or attacks something).

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `once` | `false` | Only trigger once per entity lifetime |

## Context Variables

- `@Attacker` - The entity that initiated combat (if available)

## Examples

```yaml
Skills:
  - animation{name=combat_ready} ~onEnterCombat
  - showbone{bone=weapon} ~onEnterCombat
```

## Common Patterns

### Combat Stance
```yaml
Skills:
  - animation{name=draw_weapon} ~onEnterCombat
  - showbone{bone=sword} ~onEnterCombat
```

### Boss Awakening
```yaml
Skills:
  - animation{name=awaken} ~onEnterCombat{once=true}
  - showbone{bone=glowing_eyes} ~onEnterCombat
  - hidebone{bone=sleeping_particles} ~onEnterCombat
```

### Alert Animation
```yaml
Skills:
  - animation{name=alert} ~onEnterCombat
```

### Enrage Effect
```yaml
Skills:
  - animation{name=enrage} ~onEnterCombat
  - showbone{bone=rage_aura} ~onEnterCombat
```

## Notes

- Combat state is tracked internally using a 200-tick (10 second) window after last damage
- This only fires on the transition from "not in combat" to "in combat"
- Pairs well with `~onDropCombat` for combat state management
