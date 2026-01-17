---
sidebar_position: 17
---

# ~onShoot

Fires when the entity performs a ranged attack (bow, projectile, etc.).

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `once` | `false` | Only trigger once per entity lifetime |

## Context Variables

- `@Target` - The target being shot at

## Examples

```yaml
Skills:
  - animation{name=fire_bow} ~onShoot
```

## Common Patterns

### Bow Animation
```yaml
Skills:
  - animation{name=release_arrow} ~onShoot
```

### Magic Projectile
```yaml
Skills:
  - animation{name=cast_spell} ~onShoot
  - showbone{bone=magic_circle} ~onShoot
```

### Turret Fire
```yaml
Skills:
  - animation{name=cannon_fire} ~onShoot
  - showbone{bone=muzzle_flash} ~onShoot
```

### Sniper Shot
```yaml
Skills:
  - animation{name=snipe} ~onShoot
  - hidebone{bone=scope_glow} ~onShoot
```

## Notes

- Works with any ranged attack type (bow, generic projectile, etc.)
- Fires before the projectile is actually spawned
- Only for entities using `RangedAttackMob` interface
