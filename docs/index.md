---
title: Godot Basics – 2D Jump and Run
---

# Goal

In this tutorial, you will learn how to create a simple 2D jump-and-run game in Godot.  
We will build a small Mario-style prototype to understand the basic concepts of Godot.

# Previous Knowledge

We'll assume you:

- Have Godot installed (Version 4.x)
- Know basic programming concepts (variables, functions, if-statements)
- Can create a new Godot project

# What you'll learn

In this tutorial, you will learn:

- How Scenes and Nodes work in Godot
- How to create a Player using CharacterBody2D
- How to add movement and jumping
- How to use collisions
- How to create coins using Area2D and signals
- How to restart the game when the player falls

# Tutorial

## 1. Create the Player

Create a new scene and add:

- CharacterBody2D
- Sprite2D
- CollisionShape2D

Rename the root node to `Player`.

---

## 2. Add Movement Script

Attach a script to the Player:

```csharp
using Godot;

public partial class Player : CharacterBody2D
{
    private float speed = 200f;
    private float jumpVelocity = -400f;
    private float gravity = 900f;

    public override void _PhysicsProcess(double delta)
    {
        Vector2 velocity = Velocity;

        // Gravity
        if (!IsOnFloor())
            velocity.Y += gravity * (float)delta;

        // Left & Right movement
        if (Input.IsActionPressed("move_right"))
            velocity.X = speed;
        else if (Input.IsActionPressed("move_left"))
            velocity.X = -speed;
        else
            velocity.X = 0;

        // Jump
        if (Input.IsActionJustPressed("jump") && IsOnFloor())
            velocity.Y = jumpVelocity;

        Velocity = velocity;
        MoveAndSlide();
    }
}
