---
sidebar_position: 18
---

# ~onExplode

Fires just before an entity with explosion behavior explodes. Only works for entities configured with the explosion/creeper-like behavior.

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `once` | `true` | Only trigger once (default true since explosions typically kill the entity) |

## Examples

```yaml
Skills:
  - animation{name=explode} ~onExplode
  - showbone{bone=explosion_particles} ~onExplode
```

## Common Patterns

### Explosion Warning
```yaml
Skills:
  - animation{name=swell_final} ~onExplode
  - showbone{bone=glow_effect} ~onExplode
```

### Custom Creeper
```yaml
Skills:
  - animation{name=detonate} ~onExplode
  - damage{amount=20, type=explosion} @PlayersInRadius{r=6} ~onExplode
```

### Suicide Bomber
```yaml
Skills:
  - hidebone{bone=body} ~onExplode
  - showbone{bone=explosion_debris} ~onExplode
```

## Notes

- Only fires for entities with explosion behavior configured (like creeper-style mobs)
- Fires immediately before the actual explosion occurs
- The entity is typically killed by the explosion after this trigger
