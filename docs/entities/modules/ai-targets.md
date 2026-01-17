---
sidebar_position: 4
---

# AI Targets

Define what entities your mob will target for attacks.

## Syntax

```yaml
AITargets:
  - nearestplayer
  - hurtbytarget{alertallies=true}
  - 1 nearestplayer              # With explicit priority
  - 2 hurtbytarget               # Lower priority (runs after 1)
```

**Priority Syntax:** `X targetname` or `X targetname{params}` where X is the priority number.
Lower numbers run first.

## Target Types

### nearestplayer

Targets the nearest player within range.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| mustsee | boolean | true | Requires line of sight to target |

**Priority:** 1

```yaml
- nearestplayer
- nearestplayer{mustsee=false}   # Can sense through doors (like zombies)
```

:::tip
Set `mustsee=false` for mobs that should detect players through closed doors, like zombies breaking down doors.
:::

### hurtbytarget

Targets whatever entity last attacked this mob.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| alertallies | boolean | false | Alert nearby mobs of the same type |

**Priority:** 2

```yaml
- hurtbytarget
- hurtbytarget{alertallies=true}
```

### nearestattackable

Targets the nearest entity of a specific type. Much more flexible than `nearestplayer`.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| targettype | string | player | Type of entity to target (see list below) |
| mustsee | boolean | true | Must have line of sight to target |
| mustreach | boolean | false | Must be able to path to target |
| interval | int | 10 | Ticks between target scans |

**Priority:** 2

**Valid target types:**
- `player` - Players
- `monster` - All hostile mobs
- `animal` - All passive animals
- `livingentity` - Any living entity
- Specific mobs: `zombie`, `skeleton`, `creeper`, `spider`, `enderman`, `witch`, `slime`, `phantom`, `blaze`, `ghast`, `villager`, `irongolem`, `snowgolem`, `wolf`, `cat`, `pig`, `cow`, `sheep`, `chicken`, `horse`, `goat`

```yaml
- nearestattackable{targettype=player}
- nearestattackable{targettype=monster, mustsee=true}
- nearestattackable{targettype=animal, interval=20}
```

---

## Pet Targets

These targets work with the [Taming](/docs/entities/modules/taming.md) module for pet behavior.

### ownerhurtby

Targets entities that hurt the pet's owner. Makes pets defensive.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 1

```yaml
- ownerhurtby
```

### ownerhurt

Targets entities that the pet's owner attacked. Makes pets attack what their owner attacks.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 2

```yaml
- ownerhurt
```

:::tip
Use both `ownerhurtby` and `ownerhurt` together for full pet combat support:
```yaml
AITargets:
  - ownerhurtby   # Defend owner
  - ownerhurt     # Attack owner's targets
```
:::

---

## Animal Targets

### nontamerandom

Targets random entities of a type, but only when the mob is not tamed. Useful for wild predators that become docile when tamed.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| targettype | string | animal | Type of entity to target |

**Priority:** 3

**Valid target types:** `player`, `monster`, `animal`, `livingentity`, `wolf`, `cat`, `pig`, `cow`, `sheep`, `chicken`

```yaml
- nontamerandom{targettype=chicken}
- nontamerandom{targettype=animal}
```

---

## Priority System

Targets are checked based on priority (lower = checked first):

| Priority | Target |
|----------|--------|
| 1 | nearestplayer, ownerhurtby |
| 2 | hurtbytarget, nearestattackable, ownerhurt |
| 3 | nontamerandom |

Override with priority prefix syntax:
```yaml
- 1 hurtbytarget
- 2 nearestplayer
```

---

## Examples

### Hostile
Attacks players on sight:
```yaml
AITargets:
  - nearestplayer
```

### Door Breaker (Zombie-like)
Can sense players through doors and break them down:
```yaml
AIGoals:
  - float
  - breakdoor{breaktime=120}
  - meleeattack
  - wateravoidingrandomstroll
AITargets:
  - nearestplayer{mustsee=false}   # Senses through doors
```

### Neutral
Only attacks when provoked:
```yaml
AITargets:
  - hurtbytarget
```

### Hostile + Retaliates
Attacks players and retaliates against other attackers:
```yaml
AITargets:
  - nearestplayer
  - hurtbytarget
```

### Pack Animal
Alerts allies when attacked:
```yaml
AITargets:
  - hurtbytarget{alertallies=true}
```

### Monster Hunter
Attacks hostile mobs:
```yaml
AITargets:
  - nearestattackable{targettype=monster}
```

### Predator
Hunts passive animals:
```yaml
AITargets:
  - nearestattackable{targettype=animal, mustsee=true}
```

### Tameable Pet
Defends and assists owner when tamed:
```yaml
Taming:
  enabled: true
  item: bone
AITargets:
  - ownerhurtby
  - ownerhurt
```

### Wild Predator (Tames to Docile)
Hunts animals when wild, stops hunting when tamed:
```yaml
Taming:
  enabled: true
  item: raw_beef
AITargets:
  - nontamerandom{targettype=chicken}
  - hurtbytarget
```

---

## Complete Example

```yaml
pack_wolf:
  Model: wolf_model
  Display: '&7Pack Wolf'
  Health: 20
  Damage: 4
  Taming:
    enabled: true
    item: bone
  AIGoals:
    - float
    - sitwhenordered
    - followowner{speed=1.0, teleportdistance=12}
    - leapattarget{leapheight=0.4}
    - meleeattack{speed=1.3}
    - randomstroll
    - lookatplayer
  AITargets:
    - ownerhurtby
    - ownerhurt
    - nontamerandom{targettype=chicken}
    - hurtbytarget{alertallies=true}
```

This creates a wolf that:
- Can be tamed with bones
- Sits when right-clicked by owner
- Follows and teleports to owner
- Leaps at targets
- Defends owner when they're attacked
- Attacks what owner attacks
- Hunts chickens when wild (stops when tamed)
- Alerts nearby pack wolves when attacked
