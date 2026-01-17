---
sidebar_position: 8
---

# Presets

Presets are convenience bundles that configure multiple settings at once to replicate vanilla mob behaviors. They support **all modules** and use intelligent deep-merging so you only need to specify what you want to change.

## Basic Usage

```yaml
my_skeleton:
  Model: bone_knight
  Preset: skeleton
```

That's it! The preset handles AnimationStyle, Hitbox, Traits, AIGoals, AITargets, Equipment, and more automatically.

## Deep-Merge System

Presets use intelligent merging so you can override just the parts you need:

### Scalars (Health, Damage, etc.)
Entity values override preset values.

```yaml
tank_zombie:
  Model: armored_zombie
  Preset: zombie
  Health: 100   # Override: 100 instead of preset's 20
  # Damage stays at preset's 3
```

### Maps (Hitbox, Equipment, etc.)
Maps are deep-merged - your values override specific keys while keeping others.

```yaml
tall_zombie:
  Model: tall_zombie
  Preset: zombie
  Hitbox:
    height: 2.5   # Override height
    # copy: minecraft:zombie still applies from preset
```

### Lists (AIGoals, Traits, etc.)
Lists **replace** by default - if you define AIGoals, the preset's goals are ignored.

```yaml
melee_skeleton:
  Model: bone_warrior
  Preset: skeleton
  AIGoals:              # Replace preset's ranged goals
    - float
    - meleeattack
    - randomstroll
```

### Appending to Lists
Use `Key+:` to **append** to a preset's list instead of replacing:

```yaml
fire_zombie:
  Model: fire_zombie
  Preset: zombie
  Traits+:              # Append to preset's traits
    - fireimmune        # Result: [sunburn, fireimmune]
```

## Merge Behavior Summary

| Type | Behavior | Example |
|------|----------|---------|
| Scalar | Override | `Health: 100` replaces preset's health |
| Map | Deep-merge | `Hitbox.height` overrides, `Hitbox.copy` kept |
| List | Replace | `AIGoals:` replaces preset's goals entirely |
| List with + | Append | `Traits+:` adds to preset's traits |

---

## Built-in Presets

All built-in presets include proper `Hitbox.copy` to match vanilla mob dimensions.

### skeleton

Ranged bow attack, burns in sun.

```yaml
Preset: skeleton
```

**Includes:**
- AnimationStyle: Skeleton
- Health: 20, Damage: 2
- Hitbox: copy from minecraft:skeleton
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
- Hitbox: copy from minecraft:zombie
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
- Hitbox: copy from minecraft:creeper
- AIGoals: swell (radius=3, fuse=30), meleeattack, etc.

### spider

Climbs walls, leaps at targets.

```yaml
Preset: spider
```

**Includes:**
- AnimationStyle: Spider
- Health: 16, Damage: 2
- Hitbox: copy from minecraft:spider
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
- Hitbox: copy from minecraft:cow
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
- Hitbox: copy from minecraft:pig
- AIGoals: panic, tempt (carrot), etc.

### chicken

Passive, temptable with seeds.

```yaml
Preset: chicken
```

**Includes:**
- AnimationStyle: Chicken
- Health: 4
- Hitbox: copy from minecraft:chicken
- AIGoals: panic, tempt (wheat_seeds), etc.

### wolf

Tameable, attacks skeletons.

```yaml
Preset: wolf
```

**Includes:**
- AnimationStyle: Wolf
- Health: 8, Damage: 4
- Hitbox: copy from minecraft:wolf
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
- Hitbox: copy from minecraft:blaze
- Traits: fireimmune
- AIGoals: rangedattack, etc.

### witch

Ranged potion attacks.

```yaml
Preset: witch
```

**Includes:**
- AnimationStyle: Villager
- Health: 26
- Hitbox: copy from minecraft:witch
- AIGoals: rangedattack, etc.

### slime

Bouncy melee attacker.

```yaml
Preset: slime
```

**Includes:**
- AnimationStyle: Slime
- Health: 16, Damage: 4
- Hitbox: copy from minecraft:slime
- AIGoals: meleeattack, randomstroll, etc.

### guardian

Water creature with ranged attack.

```yaml
Preset: guardian
```

**Includes:**
- AnimationStyle: Humanoid
- Health: 30
- Hitbox: copy from minecraft:guardian
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
- Hitbox: copy from minecraft:enderman
- AIGoals: meleeattack, etc.

---

## Examples

### Quick Vanilla-like Mob
```yaml
bone_warrior:
  Model: skeleton_knight
  Preset: skeleton
```

### Override Just Health
```yaml
tank_zombie:
  Model: armored_zombie
  Preset: zombie
  Health: 100  # 100 HP instead of 20
```

### Custom Hitbox Height
```yaml
tall_skeleton:
  Model: tall_skeleton
  Preset: skeleton
  Hitbox:
    height: 2.8  # Taller, but keeps skeleton width
```

### Add Traits (Append)
```yaml
fire_spider:
  Model: fire_spider
  Preset: spider
  Traits+:            # Append to [climbing]
    - fireimmune      # Result: [climbing, fireimmune]
```

### Replace AI Goals
```yaml
melee_skeleton:
  Model: bone_warrior
  Preset: skeleton
  AIGoals:            # Replace bow with melee
    - float
    - meleeattack
    - wateravoidingrandomstroll
    - lookatplayer
```

### Complex Override
```yaml
elite_zombie:
  Model: elite_zombie
  Preset: zombie
  Health: 80
  Damage: 8
  Hitbox:
    height: 2.2       # Taller
  Traits+:            # Add to sunburn
    - fireimmune
  Equipment:          # Replace equipment
    mainhand: minecraft:iron_sword
    head: minecraft:iron_helmet
```

---

## Creating Custom Presets

Create custom presets by adding YAML files in the presets directory:

**Location:** `config/modengine/entities/presets/`

**Example:** `config/modengine/entities/presets/custom.yml`

```yaml
# Custom preset supporting ALL modules
elite_guard:
  description: "Heavily armored melee fighter"
  AnimationStyle: Humanoid
  Health: 50
  Damage: 8
  Hitbox:
    copy: minecraft:iron_golem
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

# Another preset
tank:
  description: "Slow but tanky mob"
  Health: 100
  Damage: 10
  Hitbox:
    width: 1.2
    height: 2.0
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
  Health: 200  # Override preset's 100
```

---

## Preset Priority

When multiple sources define presets:

1. User presets in `config/modengine/entities/presets/` (highest priority)
2. Built-in presets shipped with ModEngine

User presets with the same name as built-in presets will override them.
