---
sidebar_position: 21
---

# ~onDespawn

Fires when an entity is removed from the world (but not killed). This includes chunk unload, `/kill` command with despawn reason, or being discarded.

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `once` | `true` | Only trigger once (default true since despawn only happens once) |

## Examples

```yaml
Skills:
  - animation{name=fade_out} ~onDespawn
```

## Common Patterns

### Fade Out Effect
```yaml
Skills:
  - animation{name=disappear} ~onDespawn
  - hidebone{bone=body} ~onDespawn
```

### Teleport Away
```yaml
Skills:
  - animation{name=teleport_out} ~onDespawn
  - showbone{bone=teleport_particles} ~onDespawn
```

### Ghost Dissipation
```yaml
Skills:
  - animation{name=dissolve} ~onDespawn
  - hidebone{bone=physical_form} ~onDespawn
```

## Notes

- Does NOT fire when the entity dies (use `~onDeath` for that)
- Fires before the entity is actually removed
- Useful for cleanup effects or visual feedback on removal
- Common causes: chunk unloading, `discard()` calls, server cleanup
