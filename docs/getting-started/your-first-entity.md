---
sidebar_position: 2
---

# Your First Entity

This guide walks you through creating a simple custom entity.

## Step 1: Add a Model

Place your model file in the models folder:

```
config/modengine/entities/models/
```

**For Blockbench models:** Place the `.bbmodel` file directly:
```
models/my_creature.bbmodel
```

**For GeckoLib models:** Create a folder with the model files:
```
models/my_creature/
├── model.geo.json
├── model.animation.json  (optional)
└── default.png
```

## Step 2: Create the Config

Create a YAML file in the entities folder:

```
config/modengine/entities/my_creature.yml
```

Add the basic configuration:

```yaml
my_creature:
  Model: my_creature
  Display: '&aFriendly Creature'
  Health: 20
  Behavior: PASSIVE
```

## Step 3: Reload and Spawn

1. Run `/mm reload` to load your new entity
2. Run `/mm spawn my_creature` to spawn it

## Adding Animations

If your model has animations, use the Skills system:

```yaml
my_creature:
  Model: my_creature
  Display: '&aFriendly Creature'
  Health: 20
  Behavior: PASSIVE
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
```

## Making it Hostile

Change the behavior and add damage:

```yaml
my_creature:
  Model: my_creature
  Display: '&cAggressive Creature'
  Health: 30
  Damage: 6
  Behavior: HOSTILE
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
    - animation{name=attack} ~onHurt
```

## Next Steps

- Learn about [basic options](../entities/basic-options)
- Set up [custom AI](../entities/ai-goals)
- Create [skills and abilities](../entities/skills/overview)
