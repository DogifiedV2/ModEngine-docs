---
sidebar_position: 2
---

# @Attacker

Targets the entity that last attacked this entity.

## Parameters

None.

## Notes

- Only works with triggers that involve being attacked (like `~onHurt`)
- Has no effect with triggers like `~onSpawn` or `~idle`
- If no attacker exists, the skill is skipped

## Examples

```yaml
Skills:
  # Reflect damage to attacker
  - damage{amount=3, type=magic} @Attacker ~onHurt

  # Counter-attack with fire on heavy hits
  - damage{amount=5, type=fire} @Attacker ~onHurt{min=10}
```

## Common Patterns

### Thorns Effect
```yaml
Skills:
  - damage{amount=2} @Attacker ~onHurt
```

### Scaling Retaliation
```yaml
Skills:
  # Small hits = small retaliation
  - damage{amount=1} @Attacker ~onHurt{max=5}

  # Big hits = big retaliation
  - damage{amount=5, type=magic} @Attacker ~onHurt{min=10}
```

### Enraged Counter-Attack
```yaml
Skills:
  # Normal retaliation
  - damage{amount=2} @Attacker ~onHurt

  # Extra damage when low health
  - damage{amount=5, type=fire} @Attacker ~onHurt ~health{below=25}
```
