---
sidebar_position: 1
---

# Animation Styles

The `AnimationStyle` property applies procedural animation based on vanilla mob movement. Name your model's bones to match the required names below.

## Usage

```yaml
my_entity:
  Model: my_model
  AnimationStyle: Zombie
```

---

## Humanoid

**Mobs:** Player, Zombie, Skeleton, Husk, Drowned, Stray, Wither_Skeleton, Piglin, Zombified_Piglin, Piglin_Brute, Pillager, Vindicator, Evoker, Illusioner

| Bone | Description |
|------|-------------|
| `head` | Rotates to look at targets |
| `body` | Torso (no animation) |
| `left_arm` | Swings opposite to left leg |
| `right_arm` | Swings opposite to right leg |
| `left_leg` | Swings while walking |
| `right_leg` | Swings while walking |

---

## Quadruped

**Mobs:** Pig, Cow, Sheep, Goat, Wolf, Fox, Cat, Ocelot, Horse, Donkey, Mule, Polar_Bear, Panda, Mooshroom

| Bone | Description |
|------|-------------|
| `head` | Rotates to look at targets |
| `body` | Torso (no animation) |
| `left_front_leg` | Front left leg |
| `right_front_leg` | Front right leg |
| `left_hind_leg` | Back left leg |
| `right_hind_leg` | Back right leg |

Diagonal pairs move together (front-right + back-left).

---

## Spider

**Mobs:** Spider, Cave_Spider

| Bone | Description |
|------|-------------|
| `head` | Limited rotation |
| `body` | Thorax (no animation) |
| `leg0` | Right front |
| `leg1` | Left front |
| `leg2` | Right second |
| `leg3` | Left second |
| `leg4` | Right third |
| `leg5` | Left third |
| `leg6` | Right back |
| `leg7` | Left back |

```
Front
  0   1
  2   3
  4   5
  6   7
Back
```

---

## Chicken

**Mobs:** Chicken, Parrot

| Bone | Description |
|------|-------------|
| `head` | Bobs while walking + rotates |
| `body` | Torso (no animation) |
| `left_wing` | Flaps subtly |
| `right_wing` | Flaps subtly |
| `left_leg` | Swings while walking |
| `right_leg` | Swings while walking |

---

## Creeper

**Mobs:** Creeper

| Bone | Description |
|------|-------------|
| `head` | Rotates to look at targets |
| `body` | Torso (no animation) |
| `left_front_leg` | Front left leg |
| `right_front_leg` | Front right leg |
| `left_hind_leg` | Back left leg |
| `right_hind_leg` | Back right leg |

Same as quadruped but no arms.

---

## Villager

**Mobs:** Villager, Witch, Wandering_Trader, Zombie_Villager

| Bone | Description |
|------|-------------|
| `head` | Rotates to look at targets |
| `body` | Torso (no animation) |
| `arms` | Crossed arms (slight sway) |
| `left_leg` | Swings while walking |
| `right_leg` | Swings while walking |

---

## Iron_Golem

**Mobs:** Iron_Golem

| Bone | Description |
|------|-------------|
| `head` | Slow rotation |
| `body` | Torso (no animation) |
| `left_arm` | Heavy swing |
| `right_arm` | Heavy swing |
| `left_leg` | Slow, heavy steps |
| `right_leg` | Slow, heavy steps |

---

## Snow_Golem

**Mobs:** Snow_Golem

| Bone | Description |
|------|-------------|
| `head` | Rotates to look |
| `body` | Torso (no animation) |
| `left_arm` | Subtle sway |
| `right_arm` | Subtle sway |

---

## Slime

**Mobs:** Slime, Magma_Cube

| Bone | Description |
|------|-------------|
| `body` | Main body (no rotation) |

---

## Notes

- Bone names are **case-insensitive**
- Missing bones are silently skipped
- Bones can be nested (e.g., arms under body)
- Keyframe animations from Skills add on top of procedural animations
