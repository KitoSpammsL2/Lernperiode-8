---
title: Godot Basics – 2D Jump-and-Run (Mario-Style)
---

# Goal

In this tutorial, you will learn the basics of Godot by creating a small 2D jump-and-run game (Mario-style).
We will build a playable prototype with:

- Player movement (left/right)
- Jumping + gravity
- Collisions (ground, platforms)
- Coins (collectibles) with animation
- Moving platforms
- Death / restart using a KillZone

# Previous Knowledge

We'll assume you:

- Have **Godot 4** installed
- Know basic programming ideas (variables, if, functions)
- Can open a Godot project and press **Play**

# What you'll learn

After this tutorial you understand:

- What **Scenes** and **Nodes** are in Godot
- How to build a Player with **CharacterBody2D**
- How **_physics_process()**, gravity and **move_and_slide()** work
- How to use **Area2D + Signals** for coins and kill zones
- How to structure a small project cleanly

# Tutorial

## 1) Godot basics: Scenes, Nodes, Inspector

Godot projects are built from **Scenes**.  
A Scene is a tree of **Nodes** (each node has a job).

Example idea for this project:

- `game.tscn` = main level scene
- `player.tscn` = player object
- `coin.tscn` = collectible coin
- `platform.tscn` = moving platform
- `killzone.tscn` = restarts the game when player touches it

**Inspector**: You can change values live (position, scale, exported variables, collision settings).

> TODO: Screenshot Node tree (optional)

---

## 2) Input Map (controls)

Open:

**Project → Project Settings → Input Map**

Create these actions:

- `move_left` (A / Left Arrow)
- `move_right` (D / Right Arrow)
- `jump` (Space)

This way your code works on any keyboard and you can easily change controls later.

---

## 3) Player Scene (CharacterBody2D)

Create `player.tscn`:

**Root node:** `CharacterBody2D`  
Add children:

- `Sprite2D`
- `CollisionShape2D`

Why this matters:
- Without `CollisionShape2D` you will fall through the ground.
- `CharacterBody2D` is made for player movement and collisions.

Attach a script named `player.gd` to the Player.

### Player movement + jump (GDScript)

```gdscript
extends CharacterBody2D

@export var speed := 200.0
@export var jump_velocity := -400.0
@export var gravity := 900.0

func _physics_process(delta: float) -> void:
	# Gravity
	if not is_on_floor():
		velocity.y += gravity * delta

	# Left / Right
	var direction := Input.get_axis("move_left", "move_right")
	velocity.x = direction * speed

	# Jump
	if Input.is_action_just_pressed("jump") and is_on_floor():
		velocity.y = jump_velocity

	move_and_slide()
