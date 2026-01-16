---
sidebar_position: 1
slug: /
---

# Introduction

ModEngine is a Minecraft mod that lets you create custom entities with dynamic models, animations, and AI behaviors using simple YAML configuration files.

## Features

- **Custom Entities** - Create mobs with custom models, animations, and behaviors
- **Multiple Model Formats** - Supports Blockbench (.bbmodel) and GeckoLib (.geo.json) models
- **Procedural Animation** - Apply vanilla-style animations based on mob type
- **Custom AI** - Define AI goals and targeting behavior
- **Skills System** - Create reactive behaviors with triggers and actions
- **Tameable Pets** - Make entities that can be tamed and follow players

## Quick Example

```yaml
my_zombie:
  Model: zombie_model
  Display: '&cCustom Zombie'
  Health: 40
  Damage: 8
  Behavior: HOSTILE
  Skills:
    - animation{name=idle, mode=loop} ~idle
    - animation{name=walk, mode=loop} ~moving
```

## Getting Started

1. [Install the mod](getting-started/installation)
2. [Create your first entity](getting-started/your-first-entity)

## Config Location

All configuration files go in your Minecraft instance's config folder:

```
config/modengine/
├── entities/           # Entity YAML configs
│   └── models/         # Model files (.bbmodel or folders)
└── items/              # Item configs (coming soon)
```
