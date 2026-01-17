---
sidebar_position: 7
---

# Traits

Traits are passive properties that are always active on your entity. Unlike AI goals (which involve decision-making), traits define what your entity **is**.

## Syntax

```yaml
Traits:
  - sunburn
  - climbing
  - fireimmune
```

## Available Traits

### sunburn

Makes the entity burn in direct sunlight (like zombies and skeletons).

```yaml
Traits:
  - sunburn
```

**Behavior:**
- Entity catches fire when exposed to direct sunlight
- Wearing a helmet protects from burning (helmet takes durability damage)
- Works during daytime when the sky is visible

:::tip
Combine with `restrictsun` and `fleesun` AI goals for complete undead behavior:
```yaml
Traits:
  - sunburn
AIGoals:
  - restrictsun
  - fleesun{speed=1.2}
```
:::

### climbing

Allows the entity to climb walls (like spiders).

```yaml
Traits:
  - climbing
```

**Behavior:**
- Entity can walk up vertical surfaces when touching them
- Works on any solid block
- No special animation required (entity walks up walls)

### fireimmune

Makes the entity immune to all fire damage.

```yaml
Traits:
  - fireimmune
```

**Behavior:**
- Immune to fire damage
- Immune to lava damage
- Cannot be set on fire
- Useful for nether mobs or fire elementals

### waterbreathing

Allows the entity to breathe underwater indefinitely.

```yaml
Traits:
  - waterbreathing
```

**Behavior:**
- No drowning damage
- Can stay underwater forever
- Useful for aquatic or amphibious mobs

### freezeimmune

Makes the entity immune to freezing in powder snow.

```yaml
Traits:
  - freezeimmune
```

**Behavior:**
- No freeze damage from powder snow
- Freeze meter doesn't accumulate
- Useful for ice/snow themed mobs

---

## Examples

### Undead Mob
```yaml
my_zombie:
  Model: zombie_model
  AnimationStyle: Zombie
  Traits:
    - sunburn
  AIGoals:
    - float
    - restrictsun
    - fleesun{speed=1.2}
    - meleeattack
    - wateravoidingrandomstroll
  AITargets:
    - nearestplayer
```

### Spider-like Mob
```yaml
wall_crawler:
  Model: spider_model
  AnimationStyle: Spider
  Traits:
    - climbing
  AIGoals:
    - float
    - leapattarget{leapheight=0.4}
    - meleeattack
    - wateravoidingrandomstroll
  AITargets:
    - nearestplayer
```

### Nether Mob
```yaml
fire_demon:
  Model: demon_model
  AnimationStyle: Humanoid
  Traits:
    - fireimmune
  AIGoals:
    - float
    - meleeattack{speed=1.2}
    - randomstroll
  AITargets:
    - nearestplayer
```

### Aquatic Mob
```yaml
sea_creature:
  Model: fish_model
  AnimationStyle: Humanoid
  Traits:
    - waterbreathing
  AIGoals:
    - randomswim{speed=1.2}
    - tryfindwater
  AITargets: []
```

### Multi-Trait Mob
```yaml
frost_spider:
  Model: ice_spider
  AnimationStyle: Spider
  Traits:
    - climbing
    - freezeimmune
    - waterbreathing
  AIGoals:
    - float
    - leapattarget
    - meleeattack
    - wateravoidingrandomstroll
  AITargets:
    - nearestplayer
```

---

## Traits vs AI Goals

| Concept | Purpose | Examples |
|---------|---------|----------|
| **Traits** | What the entity IS (passive properties) | sunburn, climbing, fireimmune |
| **AI Goals** | What the entity DOES (active decisions) | meleeattack, randomstroll, fleesun |

Traits are always active and don't require AI decision-making. For example, the `climbing` trait allows wall climbing whenever the entity touches a wall - no goal needed.

---

## Combining with Presets

If you use a [Preset](/docs/entities/modules/presets), the preset's traits apply unless you override them:

```yaml
# Uses skeleton preset's sunburn trait
my_skeleton:
  Model: bone_knight
  Preset: skeleton

# Override with custom traits (replaces preset's traits)
my_skeleton:
  Model: bone_knight
  Preset: skeleton
  Traits:
    - climbing
    - fireimmune
```
