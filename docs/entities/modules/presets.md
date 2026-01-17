---
sidebar_position: 8
---

# Presets

Presets are convenience bundles that configure multiple settings at once to replicate vanilla mob behaviors. Use them to quickly create entities that behave like vanilla mobs.

## Syntax

```yaml
my_skeleton:
  Model: bone_knight
  Preset: skeleton
```

That's it! The preset handles AnimationStyle, Traits, AIGoals, AITargets, and Equipment automatically.

## How Presets Work

Presets apply **default values** that you can override:

```yaml
my_skeleton:
  Model: bone_knight
  Preset: skeleton      # Sets all skeleton defaults
  Health: 60            # Override preset's health (20 -> 60)
  AIGoals:              # Override preset's goals entirely
    - meleeattack       # Now uses melee instead of bow
    - randomstroll
```

| If you define... | Preset... |
|------------------|-----------|
| Nothing | Applies all its defaults |
| `Health` | Uses your health, applies everything else |
| `AIGoals` | Uses your goals, skips preset's goals |
| `Traits` | Uses your traits, skips preset's traits |

---

## Built-in Presets

### skeleton

Ranged bow attack, burns in sun.

```yaml
Preset: skeleton
```

**Includes:**
- AnimationStyle: Skeleton
- Health: 20, Damage: 2
- Traits: sunburn
- AIGoals: rangedbowattack, fleesun, restrictsun, etc.
- Equipment: bow in main hand

### zombie

Melee attack, burns in sun, breaks doors.

```yaml
Preset: zombie
```

**Includes:**
- AnimationStyle: Zombie
- Health: 20, Damage: 3
- Traits: sunburn
- AIGoals: breakdoor, meleeattack, fleesun, restrictsun, etc.

### creeper

Swells and explodes near players.

```yaml
Preset: creeper
```

**Includes:**
- AnimationStyle: Creeper
- Health: 20
- AIGoals: swell (radius=3, fuse=30), meleeattack, etc.

### spider

Climbs walls, leaps at targets.

```yaml
Preset: spider
```

**Includes:**
- AnimationStyle: Spider
- Health: 16, Damage: 2
- Traits: climbing
- AIGoals: leapattarget, meleeattack, etc.

### cow

Passive, temptable with wheat.

```yaml
Preset: cow
```

**Includes:**
- AnimationStyle: Cow
- Health: 10
- AIGoals: panic, tempt (wheat), etc.
- No attack targets

### pig

Passive, temptable with carrot.

```yaml
Preset: pig
```

**Includes:**
- AnimationStyle: Pig
- Health: 10
- AIGoals: panic, tempt (carrot), etc.

### chicken

Passive, temptable with seeds.

```yaml
Preset: chicken
```

**Includes:**
- AnimationStyle: Chicken
- Health: 4
- AIGoals: panic, tempt (wheat_seeds), etc.

### wolf

Tameable, attacks skeletons.

```yaml
Preset: wolf
```

**Includes:**
- AnimationStyle: Wolf
- Health: 8, Damage: 4
- AIGoals: sitwhenordered, followowner, leapattarget, meleeattack, etc.
- AITargets: ownerhurtby, ownerhurt, skeleton

### blaze

Fire immune, ranged attacks.

```yaml
Preset: blaze
```

**Includes:**
- AnimationStyle: Humanoid
- Health: 20, Damage: 6
- Traits: fireimmune
- AIGoals: rangedattack, etc.

### slime

Bouncy melee attacker.

```yaml
Preset: slime
```

**Includes:**
- AnimationStyle: Slime
- Health: 16, Damage: 4
- AIGoals: meleeattack, randomstroll, etc.

### guardian

Water creature with ranged attack.

```yaml
Preset: guardian
```

**Includes:**
- AnimationStyle: Humanoid
- Health: 30
- Traits: waterbreathing
- AIGoals: rangedattack, randomswim, etc.

### enderman

Tall hostile mob.

```yaml
Preset: enderman
```

**Includes:**
- AnimationStyle: Humanoid
- Health: 40, Damage: 7
- AIGoals: meleeattack, etc.

---

## Examples

### Quick Vanilla-like Mob
```yaml
bone_warrior:
  Model: skeleton_knight
  Preset: skeleton
```

### Custom Model with Vanilla Behavior
```yaml
demon_spider:
  Model: demon_spider_model
  Preset: spider
  Health: 30
  Damage: 5
```

### Override Just One Thing
```yaml
tank_zombie:
  Model: armored_zombie
  Preset: zombie
  Health: 100  # Tanky zombie with 100 HP instead of 20
```

### Mix Behaviors (Override Goals)
```yaml
exploding_skeleton:
  Model: bomb_skeleton
  Preset: skeleton
  AIGoals:
    - float
    - swell{radius=2, fuse=20}  # Explodes instead of shooting
    - meleeattack
    - wateravoidingrandomstroll
  AITargets:
    - nearestplayer
```

### Completely Custom with Starting Point
```yaml
ice_demon:
  Model: frost_demon
  Preset: blaze  # Start with blaze as base
  Traits:
    - freezeimmune  # Override: ice instead of fire
  AIGoals:
    - float
    - rangedattack{attackInterval=40}
    - randomstroll
```

---

## Creating Custom Presets

You can create custom presets by adding YAML files in the presets directory:

**Location:** `config/modengine/entities/presets/`

Any `.yml` or `.yaml` files in this directory will be loaded as presets.

**Example:** `config/modengine/entities/presets/custom.yml`

```yaml
# Custom preset
elite_guard:
  description: "Heavily armored melee fighter"
  AnimationStyle: Humanoid
  Health: 50
  Damage: 8
  AIGoals:
    - float
    - meleeattack{speed=1.2}
    - movetowardstarget{speed=1.0}
    - wateravoidingrandomstroll
    - lookatplayer
  AITargets:
    - hurtbytarget
    - nearestplayer
  Equipment:
    mainhand: minecraft:iron_sword
    head: minecraft:iron_helmet
    chest: minecraft:iron_chestplate

# Another preset in the same file
tank:
  description: "Slow but tanky mob"
  Health: 100
  Damage: 10
  AIGoals:
    - meleeattack{speed=0.6}
    - wateravoidingrandomstroll{speed=0.4}
```

Then use them:
```yaml
my_guard:
  Model: guard_model
  Preset: elite_guard

my_tank:
  Model: tank_model
  Preset: tank
```

---

## Preset Priority

When multiple sources define presets:

1. User presets in `config/modengine/entities/presets/` (highest priority)
2. Built-in presets shipped with ModEngine

User presets with the same name as built-in presets will override them.
