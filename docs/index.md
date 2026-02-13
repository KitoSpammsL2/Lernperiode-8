---
Godot 4 – 2D Platformer Tutorial
---

# Goal

In this tutorial, you will create a simple 2D platformer using Godot 4.

The game is inspired by classic Mario-style platformers and will include:

- Player movement
- Jumping with gravity
- Worldbuilding with a TileMap
- Moving platforms
- Collectible coins
- A simple death and restart system

---

# Previous Knowledge

Before starting, you should:

- Have Godot 4 installed
- Understand basic programming concepts (variables, functions, conditions)
- Know how to create and run a Godot project

---

# What you'll learn

After completing this tutorial, you will understand:

- How Scenes and Nodes work in Godot
- How to use CharacterBody2D for movement
- How gravity and jumping are implemented
- How to use Area2D and signals
- How to restart a scene
- How to structure a simple 2D game project

---

# Player 1.0

We start by creating the player.

## Scene Setup

Create a new scene called `player.tscn`.

Root node:

- `CharacterBody2D`

Add the following child nodes:

- `Sprite2D`
- `CollisionShape2D`

The `CharacterBody2D` node is designed for characters that move and collide using physics.

---

## Player Movement Script

Attach a script called `player.gd`.

```gdscript
extends CharacterBody2D

const SPEED = 130.0
const JUMP_VELOCITY = -350.0

func _physics_process(delta: float) -> void:

	# Apply gravity
	if not is_on_floor():
		velocity += get_gravity() * delta

	# Jump
	if Input.is_action_just_pressed("jump") and is_on_floor():
		velocity.y = JUMP_VELOCITY

	# Horizontal movement
	var direction := Input.get_axis("left", "right")

	if direction:
		velocity.x = direction * SPEED
	else:
		velocity.x = move_toward(velocity.x, 0, SPEED)

	move_and_slide()
```

This script handles:

- Gravity  
- Jumping  
- Smooth left and right movement  

---

# Input Map Setup

Open:

Project → Project Settings → Input Map

Add the following actions:

- `left`
- `right`
- `jump`

Assign keys such as:

- A / D  
- Arrow keys  
- Space  

Without setting up the Input Map correctly, movement will not work.

---

# Worldbuilding 1.0

Now we create the level.

## TileMap

Open your main scene (for example `game.tscn`).

Add a `TileMap` node.

Import or create a Tileset and make sure:

- Collision shapes are defined inside the Tileset editor.

If collision shapes are missing, the player will fall through the ground.

Use the TileMap to design a simple platform layout.

---

# Platforms

To make the level more dynamic, we add moving platforms.

## Platform Scene

Create a new scene called `platform.tscn`.

Root node:

- `AnimatableBody2D`

Add:

- `Sprite2D`
- `CollisionShape2D`
- `AnimationPlayer`

## Platform Movement

Using the `AnimationPlayer`:

1. Create a new animation.  
2. Animate the platform’s position.  
3. Enable looping.  

This creates a back-and-forth movement typical for platformer games.

---

# Pickups (Coins)

Next, we add collectibles.

## Coin Scene

Create `coin.tscn`.

Root node:

- `Area2D`

Add:

- `Sprite2D`
- `CollisionShape2D`

Connect the `body_entered` signal to a script.

Attach `coin.gd`:

```gdscript
extends Area2D

func _on_body_entered(body: Node2D) -> void:
	print("+1 coin")
	queue_free()



```

n is not set to loop.
