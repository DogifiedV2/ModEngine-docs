---
sidebar_position: 20
---

# ~onLoad

Fires when an entity is loaded from save data (chunk load, world load, etc.).

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `once` | `false` | Only trigger once per entity lifetime |

## Examples

```yaml
Skills:
  - animation{name=wake_up} ~onLoad
```

## Common Patterns

### Wake Up Animation
```yaml
Skills:
  - animation{name=stretch} ~onLoad
```

### Restore Visual State
```yaml
Skills:
  - showbone{bone=equipment} ~onLoad
  - animation{name=idle} ~onLoad
```

### Re-initialization
```yaml
Skills:
  - hidebone{bone=death_particles} ~onLoad
  - showbone{bone=living_effects} ~onLoad
```

## Notes

- Different from `~onSpawn` - this fires when loading existing entities
- `~onSpawn` fires when the entity is first created
- `~onLoad` fires when the entity is loaded from NBT data
- Useful for restoring visual states that may not persist through save/load
