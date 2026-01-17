---
sidebar_position: 12
---

# ~onInteract

Fires when a player right-clicks on the entity. Useful for NPCs, quest mobs, and interactive creatures.

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `once` | `false` | Only trigger once per entity lifetime |
| `cooldown` | `0` | Minimum ticks between triggers (prevents spam) |

## Context Variables

- `@TriggerSource` - The player who interacted

## Examples

```yaml
Skills:
  - animation{name=wave} ~onInteract
  - animation{name=talk} ~onInteract{cooldown=40}
```

## Common Patterns

### NPC Greeting
```yaml
Skills:
  - animation{name=wave} ~onInteract{cooldown=60}
```

### Quest Giver
```yaml
Skills:
  - animation{name=talk} ~onInteract{cooldown=20}
  - showbone{bone=quest_marker} ~onInteract{once=true}
```

### Merchant Animation
```yaml
Skills:
  - animation{name=show_wares} ~onInteract{cooldown=40}
```

### One-Time Interaction
```yaml
Skills:
  - animation{name=awaken} ~onInteract{once=true}
  - showbone{bone=eyes} ~onInteract{once=true}
```

### Scared Creature
```yaml
Skills:
  - animation{name=flinch} ~onInteract
  - hidebone{bone=happy_face} ~onInteract
  - showbone{bone=scared_face} ~onInteract
```

## Notes

- Only main hand (right-click) interactions trigger this
- Interaction skills fire before taming logic if taming is enabled
- Use `cooldown` to prevent animation spam from rapid clicking
