---
sidebar_position: 19
---

# ~onSignal

Fires when the entity receives a signal. Signals enable communication between entities or from external systems.

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `signal` or `s` | `""` | Filter to only receive specific signals (empty = all signals) |
| `once` | `false` | Only trigger once per entity lifetime |

## Context Variables

- `@TriggerSource` - The entity that sent the signal (if any)
- `signal` variable contains the signal name

## Examples

```yaml
Skills:
  - animation{name=activate} ~onSignal{signal=activate}
  - animation{name=deactivate} ~onSignal{s=deactivate}
```

## Common Patterns

### Activation Signal
```yaml
Skills:
  - animation{name=power_on} ~onSignal{signal=activate}
  - showbone{bone=power_indicator} ~onSignal{signal=activate}
```

### Multi-Signal Handler
```yaml
Skills:
  - animation{name=phase1} ~onSignal{signal=phase1}
  - animation{name=phase2} ~onSignal{signal=phase2}
  - animation{name=phase3} ~onSignal{signal=phase3}
```

### Boss Coordination
```yaml
Skills:
  - animation{name=enrage} ~onSignal{signal=boss_enrage}
  - showbone{bone=enrage_aura} ~onSignal{signal=boss_enrage}
```

### Any Signal Response
```yaml
Skills:
  - animation{name=alert} ~onSignal
```

## Sending Signals

Signals can be sent to entities via:
- Command: `/mm signal <entity-uuid> <signal-name>`
- Other mods/plugins using the `receiveSignal()` method

## Notes

- Without a signal filter, the trigger responds to any signal
- Signal names are case-insensitive
- Useful for coordinating boss mechanics or external integrations
