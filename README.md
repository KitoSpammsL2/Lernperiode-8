# Lernperiode-8
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



## 09.01


<img width="1253" height="758" alt="image" src="https://github.com/user-attachments/assets/e733a1a9-ca82-43a4-897b-3ec3921bad13" />

Ich habe mich für Godot entschieden. Ich habe überlegt, ein Tycoon Spiel zu machen. Die Zeit in dieser kurzen Lernperiode reicht wahrscheinlich nicht aus. Deshalb habe ich mir vorgenommen, das Projekt in den Ferien fertigzumachen. Ich habe ein Tutorial angefangen. Darin wird erklärt, wie man ein Spiel mit Godot programmiert. Am Anfang ist es mir ziemlich schwer gefallen. Für mich war alles nicht sehr übersichtlich. Mit der Zeit ging es aber immer besser. 

## 16.01

-  [ ] Projekt + UI-Grundgerüst
-  [ ] C# Script anbinden + “UI Test”
-  [ ] Core Loop: Geld pro Sekunde + Kaufen/Leveln
-  [ ] Save/Load + Offline Earnings


Ich habe nichts davon gemacht, weil ich es zu schwer fand. Außerdem dauert das für nur drei Wochen viel zu lange. Ich glaube, ich habe mir da etwas zu viel vorgenommen. Deshalb habe ich mir ein neues Tutorial gesucht. Jetzt mache ich eine Art Jump-and-Run, das mich ein bisschen an Mario erinnert.

<img width="1164" height="717" alt="image" src="https://github.com/user-attachments/assets/af0cf0c8-ce8f-4f47-91e4-5c0e4065b2e2" />


## 23.01

- [x] Moving Platforms
- [x] Coins mit animation
- [x] Sterben hinzufügen
- [x] Hintergrund und Map erweitern

Heute konnte ich wieder einiges weiterentwickeln. Ich habe zum Beispiel Moving Platforms hinzugefügt und die App allgemein erweitert, damit alles besser funktioniert und mehr Spaß macht. Ausserdem habe ich Coins eingebaut, die man sammeln kann, und auch das Sterben bzw. ein Game-Over-System hinzugefügt. Dadurch fühlt sich das Spiel schon viel mehr wie ein richtiges Game an.

Ich merke immer mehr, dass mir das Arbeiten mit Godot persönlich sehr viel Spass macht, weil man schnell Fortschritte sieht und kreativ sein kann. Insgesamt bin ich mit dem heutigen Ergebnis sehr zufrieden. Ich freue mich jetzt schon darauf, nach den Ferien weiterzumachen und noch mehr Features einzubauen.

<img width="1160" height="729" alt="image" src="https://github.com/user-attachments/assets/251a010c-2fae-4131-be3a-701f7b8bb447" />



## 13.02

- [ ] Enemy hinzufügen
- [ ] Ein Score hinzufügen
- [ ] Audio hinzufügen
- [ ] Mehr Animationen hinzufügen für den PLayer. (Links, rechts)
