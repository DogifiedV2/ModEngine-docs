---
sidebar_position: 3
---

# AI Goals

Define custom AI behavior for your entity. When `AIGoals` is present, it overrides any `Behavior` preset.

## Syntax

Each goal can be simple or have parameters. You can optionally specify priority with a number prefix:

```yaml
AIGoals:
  - float                           # Simple (uses default priority)
  - meleeattack{speed=1.2}          # With parameters
  - 1 swell{radius=3}               # With explicit priority (lower = higher priority)
  - 2 meleeattack                   # Priority prefix without params
```

**Priority Syntax:** `X goalname` or `X goalname{params}` where X is the priority number.
Lower numbers run first (priority 0 runs before priority 1).

## Goal Types

### float

Keeps the entity above water.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 0

```yaml
- float
```

### panic

Makes the entity flee when hurt.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.25 | Movement speed while fleeing |

**Priority:** 1

```yaml
- panic
- panic{speed=1.5}
```

### meleeattack

Performs melee attacks on the current target.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.0 | Chase speed |
| alwaysfollow | boolean | false | Follow through walls |

**Priority:** 2

```yaml
- meleeattack
- meleeattack{speed=1.2, alwaysfollow=true}
```

:::note
If you have attack goals but no `AITargets`, the entity defaults to `hurtbytarget` (only attacks when attacked first).
:::

### randomstroll

Wanders randomly when idle (avoids water).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 0.8 | Wander speed |

**Priority:** 7

```yaml
- randomstroll
- randomstroll{speed=0.5}
```

### lookatplayer

Looks at nearby players.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| range | double | 8.0 | Look range in blocks |

**Priority:** 8

```yaml
- lookatplayer
- lookatplayer{range=12.0}
```

---

## Combat Goals

### leapattarget

Leaps at the current target (like spiders and wolves).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| leapheight | float | 0.4 | Vertical velocity of the leap |

**Priority:** 4

```yaml
- leapattarget
- leapattarget{leapheight=0.5}
```

### movetowardstarget

Approaches the current target aggressively (like iron golems).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 0.9 | Movement speed |
| within | float | 32.0 | Maximum distance to start approaching |

**Priority:** 2

```yaml
- movetowardstarget
- movetowardstarget{speed=1.0, within=16}
```

### avoidentity

Flees from specified entity types (for cowardly mobs).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| target | string | player | Entity type to avoid (e.g., player, wolf, cat, ocelot) |
| distance | float | 6.0 | Distance to maintain from target |
| walkSpeed | double | 1.0 | Walking speed when avoiding |
| sprintSpeed | double | 1.2 | Sprint speed when close |

**Priority:** 1

```yaml
- avoidentity
- avoidentity{target=player, distance=8}
- avoidentity{target=wolf, distance=6, walkSpeed=1.0, sprintSpeed=1.2}
- avoidentity{target=cat, distance=6}
```

:::tip
Skeletons avoid wolves, and creepers avoid cats and ocelots in vanilla Minecraft. Use this goal to replicate that behavior.
:::

### swell

Creeper-like swelling behavior that triggers an explosion when close to targets.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| radius | int | 3 | Explosion radius in blocks |
| fuse | int | 30 | Ticks before explosion (1.5 seconds default) |
| powered | boolean | false | Whether explosion is powered (2x radius) |

**Priority:** 1

```yaml
- swell
- swell{radius=4, fuse=40}
- swell{radius=3, fuse=30, powered=true}
```

:::tip
The swell goal makes the entity start swelling when within 3 blocks of a target. If the target moves away (>7 blocks) or breaks line of sight, swelling stops.
:::

### rangedattack

Generic ranged attack behavior (like witch potion throwing).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| attackInterval | int | 60 | Ticks between attacks |
| attackRadius | double | 15.0 | Maximum attack range |
| speed | double | 1.0 | Movement speed when chasing |

**Priority:** 4

```yaml
- rangedattack
- rangedattack{attackInterval=40, attackRadius=20}
```

### rangedbowattack

Skeleton-style bow attack with strafing behavior.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.0 | Movement speed |
| attackInterval | int | 20 | Ticks between shots |
| attackRadius | float | 15.0 | Maximum attack range |

**Priority:** 4

```yaml
- rangedbowattack
- rangedbowattack{attackInterval=30, attackRadius=20}
```

:::note
The entity should have a bow equipped (`Equipment: mainhand: minecraft:bow`) for proper behavior.
:::

---

## Sun Avoidance Goals

### fleesun

Makes the entity seek shade when in sunlight.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.0 | Movement speed when fleeing |

**Priority:** 2

```yaml
- fleesun
- fleesun{speed=1.2}
```

### restrictsun

Prevents pathfinding through sunlit areas.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 0

```yaml
- restrictsun
```

:::tip
Combine `fleesun` and `restrictsun` for undead-style sun avoidance:
```yaml
- restrictsun
- fleesun{speed=1.2}
```
:::

---

## Pet Goals

These goals work with the [Taming](/docs/entities/modules/taming.md) module.

### sitwhenordered

Makes tamed pets sit when ordered by their owner.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 1

```yaml
- sitwhenordered
```

### followowner

Makes tamed pets follow their owner, with teleportation when too far.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.0 | Movement speed |
| startdistance | float | 10.0 | Distance to start following |
| stopdistance | float | 2.0 | Distance to stop following |
| teleportdistance | float | 12.0 | Distance to trigger teleport |

**Priority:** 6

```yaml
- followowner
- followowner{speed=1.2, startdistance=8, stopdistance=3, teleportdistance=15}
```

---

## Animal Behaviors

### tempt

Makes the entity follow players holding certain items.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.0 | Movement speed when following |
| items | string | wheat | Items that tempt (semicolon-separated) |
| canscare | boolean | false | Whether running scares the entity away |

**Priority:** 3

```yaml
- tempt{items=wheat}
- tempt{speed=1.2, items=wheat;carrot;potato, canscare=true}
```

### eatblock

Eats grass blocks (like sheep).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 5

```yaml
- eatblock
```

---

## Environment Goals

### breakdoor

Breaks doors (like zombies on hard difficulty).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| breaktime | int | 240 | Ticks to break door (12 seconds default) |

**Priority:** 1

```yaml
- breakdoor
- breakdoor{breaktime=120}
```

### opendoor

Opens and optionally closes doors.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| closedoor | boolean | true | Whether to close door after passing |

**Priority:** 5

```yaml
- opendoor
- opendoor{closedoor=false}
```

---

## Movement Goals

### lookaround

Randomly looks around when idle.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 9

```yaml
- lookaround
```

### followmob

Follows other nearby mobs.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.0 | Movement speed |
| stopdistance | float | 3.0 | Distance to stop following |
| areasize | float | 7.0 | Search radius for mobs to follow |

**Priority:** 6

```yaml
- followmob
- followmob{speed=1.0, stopdistance=2, areasize=10}
```

---

## Aquatic Goals

### randomswim

Swims randomly in water (for aquatic mobs).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.0 | Swimming speed |
| interval | int | 120 | Ticks between swim attempts |

**Priority:** 4

```yaml
- randomswim
- randomswim{speed=1.2, interval=80}
```

### wateravoidingrandomstroll

Wanders randomly while avoiding water.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.0 | Movement speed |
| probability | float | 0.001 | Chance per tick to start wandering |

**Priority:** 6

```yaml
- wateravoidingrandomstroll
- wateravoidingrandomstroll{speed=0.8, probability=0.002}
```

### wateravoidingrandomflying

Flies randomly while avoiding water (for flying mobs).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| speed | double | 1.0 | Flying speed |

**Priority:** 6

```yaml
- wateravoidingrandomflying
- wateravoidingrandomflying{speed=1.5}
```

### breathair

Surfaces periodically to breathe (like dolphins).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 0

```yaml
- breathair
```

### tryfindwater

Seeks water when on land (for aquatic mobs).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 1

```yaml
- tryfindwater
```

### climbpowdersnow

Climbs on top of powder snow (like goats).

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| - | - | - | No parameters |

**Priority:** 1

```yaml
- climbpowdersnow
```

---

## Priority System

Goals execute based on priority (lower number = higher priority):

| Priority | Goal |
|----------|------|
| 0 | float, breathair, restrictsun |
| 1 | panic, sitwhenordered, avoidentity, breakdoor, tryfindwater, climbpowdersnow, swell |
| 2 | meleeattack, movetowardstarget, fleesun |
| 3 | tempt |
| 4 | leapattarget, randomswim, rangedattack, rangedbowattack |
| 5 | eatblock, opendoor |
| 6 | followowner, followmob, wateravoidingrandomstroll, wateravoidingrandomflying |
| 7 | randomstroll |
| 8 | lookatplayer |
| 9 | lookaround |

Override priority on any goal using the prefix syntax:

```yaml
- 1 meleeattack              # Priority 1 (higher than default 2)
- 0 float                    # Priority 0 (runs first)
- 3 swell{radius=4}          # Priority 3 with parameters
```

---

## Examples

### Passive Mob
```yaml
AIGoals:
  - float
  - randomstroll{speed=0.6}
  - lookatplayer
```

### Hostile Mob
```yaml
AIGoals:
  - float
  - meleeattack{speed=1.2}
  - randomstroll
  - lookatplayer
AITargets:
  - nearestplayer
```

### Neutral Mob
```yaml
AIGoals:
  - float
  - meleeattack
  - randomstroll
  - lookatplayer
AITargets:
  - hurtbytarget
```

### Cowardly Mob
```yaml
AIGoals:
  - float
  - panic{speed=1.5}
  - avoidentity{distance=8}
  - randomstroll{speed=0.4}
  - lookatplayer
```

### Undead Mob (Sun Avoidance)
```yaml
AIGoals:
  - float
  - restrictsun
  - fleesun{speed=1.2}
  - meleeattack{speed=1.0}
  - randomstroll
AITargets:
  - nearestplayer
```

### Creeper-like Mob (Explodes)
```yaml
AIGoals:
  - 0 float
  - 1 swell{radius=3, fuse=30}
  - 3 meleeattack{speed=1.0}
  - 5 wateravoidingrandomstroll{speed=0.8}
  - 6 lookatplayer
AITargets:
  - 1 nearestplayer
  - 2 hurtbytarget
```

### Skeleton-like Archer
```yaml
AIGoals:
  - 0 float
  - 1 restrictsun
  - 3 fleesun{speed=1.0}
  - 4 rangedbowattack{attackInterval=20, attackRadius=15}
  - 6 wateravoidingrandomstroll{speed=1.0}
  - 7 lookatplayer
AITargets:
  - 1 hurtbytarget
  - 2 nearestplayer
Traits:
  - sunburn
Equipment:
  mainhand: minecraft:bow
```

### Pouncing Predator
```yaml
AIGoals:
  - float
  - leapattarget{leapheight=0.5}
  - meleeattack{speed=1.3}
  - randomstroll
  - lookatplayer
AITargets:
  - nearestattackable{targettype=animal}
```

### Tameable Pet
```yaml
Taming:
  enabled: true
  item: bone
AIGoals:
  - float
  - sitwhenordered
  - followowner{speed=1.0, teleportdistance=12}
  - meleeattack{speed=1.5}
  - randomstroll
AITargets:
  - ownerhurtby
  - ownerhurt
```

### Aquatic Mob
```yaml
AIGoals:
  - breathair
  - tryfindwater
  - randomswim{speed=1.2}
```

### Farm Animal
```yaml
AIGoals:
  - float
  - panic{speed=1.3}
  - tempt{items=wheat;carrot, canscare=true}
  - wateravoidingrandomstroll{speed=0.6}
  - lookaround
```
