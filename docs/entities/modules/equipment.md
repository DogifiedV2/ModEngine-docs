---
sidebar_position: 8
---

# Equipment

Equip items on your entity's equipment slots.

## Syntax

```yaml
Equipment:
  mainhand: minecraft:diamond_sword
  offhand: minecraft:shield
  head: minecraft:iron_helmet
  chest: minecraft:iron_chestplate
  legs: minecraft:iron_leggings
  feet: minecraft:iron_boots
```

## Available Slots

| Slot | Aliases | Description |
|------|---------|-------------|
| `mainhand` | `hand` | Primary hand (right hand) |
| `offhand` | - | Secondary hand (left hand) |
| `head` | `helmet` | Helmet slot |
| `chest` | `chestplate` | Chestplate slot |
| `legs` | `leggings` | Leggings slot |
| `feet` | `boots` | Boots slot |

## Item IDs

Use standard Minecraft item IDs:

```yaml
Equipment:
  mainhand: minecraft:diamond_sword
  mainhand: diamond_sword           # minecraft: prefix is optional
  mainhand: modid:custom_item       # Modded items work too
```

---

## Examples

### Armed Skeleton
```yaml
skeleton_knight:
  Model: humanoid
  Preset: skeleton
  Equipment:
    mainhand: minecraft:iron_sword
    offhand: minecraft:shield
    head: minecraft:iron_helmet
```

### Archer
```yaml
archer:
  Model: humanoid
  Health: 20
  AIGoals:
    - 0 float
    - 4 rangedbowattack{attackInterval=20, attackRadius=15}
    - 6 wateravoidingrandomstroll
  AITargets:
    - 1 nearestplayer
  Equipment:
    mainhand: minecraft:bow
```

### Full Diamond Warrior
```yaml
diamond_warrior:
  Model: humanoid
  Health: 50
  Damage: 10
  AIGoals:
    - 0 float
    - 2 meleeattack{speed=1.2}
    - 5 wateravoidingrandomstroll
  AITargets:
    - 1 nearestplayer
  Equipment:
    mainhand: minecraft:diamond_sword
    offhand: minecraft:shield
    head: minecraft:diamond_helmet
    chest: minecraft:diamond_chestplate
    legs: minecraft:diamond_leggings
    feet: minecraft:diamond_boots
```

### Sunburn Protection
Entities with the `sunburn` trait are protected if wearing a helmet:

```yaml
undead_knight:
  Model: humanoid
  Traits:
    - sunburn
  AIGoals:
    - 0 float
    - 0 restrictsun
    - 2 fleesun
    - 3 meleeattack
    - 5 wateravoidingrandomstroll
  AITargets:
    - 1 nearestplayer
  Equipment:
    head: minecraft:iron_helmet    # Protects from burning
    mainhand: minecraft:iron_sword
```

:::note
When entities with `sunburn` wear helmets, the helmet takes durability damage instead of the entity catching fire. Once the helmet breaks, the entity will burn normally.
:::

---

## Equipment from Presets

If using a [Preset](/docs/entities/modules/presets.md), the preset's equipment applies unless you override it:

```yaml
# Uses skeleton preset's bow
my_skeleton:
  Model: humanoid
  Preset: skeleton

# Override with custom equipment
my_skeleton:
  Model: humanoid
  Preset: skeleton
  Equipment:
    mainhand: minecraft:crossbow
```
