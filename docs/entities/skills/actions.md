---
sidebar_position: 2
---

# Actions

Actions define what happens when a skill triggers.

## animation

Plays an animation on the entity.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| name | string | required | Animation name from the model |
| mode | string | once | `once`, `loop`, or `hold` |
| blend | boolean | true | Blend from previous animation |

**Modes:**
- `once` - Play once then stop
- `loop` - Repeat continuously
- `hold` - Play once and hold the last frame

```yaml
Skills:
  # Loop while idle
  - animation{name=idle, mode=loop} ~idle

  # Play once when hurt
  - animation{name=hurt} ~onHurt

  # Hold pose while sitting
  - animation{name=sit, mode=hold} ~sitting

  # No blending for instant switch
  - animation{name=transform, blend=false} ~health{below=50, once=true}
```

## damage

Deals damage to targets.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| amount | number | 1.0 | Damage amount |
| type | string | generic | Damage type |

**Damage types:**
- `generic` - Normal damage
- `fire` - Fire damage
- `explosion` - Explosion damage
- `magic` - Magic damage
- `fall` - Fall damage
- `drown` - Drowning damage
- `freeze` - Freezing damage
- `lightning` - Lightning damage

```yaml
Skills:
  # Explosion on death
  - damage{amount=10, type=explosion} @PlayersInRadius{r=5} ~onDeath

  # Fire aura at low health
  - damage{amount=2, type=fire} @PlayersInRadius{r=3} ~health{below=25}

  # Reflect damage to attacker
  - damage{amount=3, type=magic} @Attacker ~onHurt
```

## hidebone

Hides a bone on the entity. Works with both GeckoLib and Blockbench models.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| bone | string | required | Bone name to hide |

```yaml
Skills:
  # Hide helmet on death
  - hidebone{bone=helmet} ~onDeath

  # Hide folded wings when moving
  - hidebone{bone=wings_folded} ~moving
```

## showbone

Shows a previously hidden bone. Works with both GeckoLib and Blockbench models.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| bone | string | required | Bone name to show |

```yaml
Skills:
  # Reveal wings at low health
  - showbone{bone=wings_extended} ~health{below=50, once=true}

  # Show enraged effects
  - showbone{bone=fire_aura} ~health{below=25, once=true}
```

## Combining Actions

Multiple actions can share the same trigger:

```yaml
Skills:
  # Phase 2 transformation at 50% health
  - animation{name=transform} ~health{below=50, once=true}
  - showbone{bone=phase2_wings} ~health{below=50, once=true}
  - showbone{bone=phase2_crown} ~health{below=50, once=true}
  - hidebone{bone=phase1_cape} ~health{below=50, once=true}
```
