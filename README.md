# Project2: Survival Shooter Game

## Game Overview
Project2 is a top-down survival shooter where the player controls a character and tries to survive as long as possible against waves of enemies. The objective is to avoid enemy contact, shoot enemies with a pistol, and maximize your score, which increases for each enemy defeated. The game ends when the player’s health reaches zero.

The gameplay focuses on fast reflexes, movement strategy, and accurate shooting. Enemies spawn randomly across the screen and chase the player using simple boid-like behavior.

---

## Controls
- **Movement:** Arrow keys or `W`, `A`, `S`, `D`
- **Shoot:** Mouse cursor + right-click
- **Start Game:** `Spacebar`
- **Restart after Game Over:** `Spacebar`

The player is represented by an `Area2D` node with a `Sprite2D` child for the visible character. The pistol is attached as a child node and rotates to face the mouse cursor.

---

## Game Mechanics
- **Health:** The player has a health bar displayed on the HUD. Colliding with enemies reduces health.
- **Enemies:** Spawn randomly and move towards the player. On death, they can spawn additional enemies (0–3).
- **Score:** Each enemy killed increases the player’s score by 1.
- **Game Flow:** The game waits for the spacebar press to start, hides the player until then, and cleans up enemies on game over.

---

## Special Features and Requirements

1. **At least two new features developed by extending `Sprite2D`:**
    - **Pistol Node**
        - Extends `Sprite2D`
        - Rotates to face the mouse cursor
        - Fires bullets toward the cursor when the player clicks
        - **Editor Parameter:** `bullet_scene` (the scene used for bullets) can be swapped in the editor
        - **Signal:** Notifies bullets when fired (internal function usage)
    - **Bullet Node**
        - Extends `Area2D` (with sprite for visuals)
        - Moves toward a target and deals damage on collision with enemies
        - **Editor Parameters:** `speed` (bullet speed) and `damage` (amount of damage to enemy)

2. **Signal emitted by a node that triggers a method in an existing node:**
    - The `Player` node emits the `died` signal when health reaches zero.
    - This signal is connected to the `Main` node’s `player_died()` method, which triggers the game over sequence.

3. **Method triggered by a signal from an existing node:**
    - The `_on_enemy_died(_enemy)` method in `Main` is triggered when the `EnemyBoid` C# node emits the `EnemyDied` signal.
    - This updates the score and spawns additional enemies dynamically.

---

## File System Overview
- **gdextension/src**: Contains all C# source files (`EnemyBoid.cs`) implementing enemy behavior.
- **scenes/**: All Godot scene files (`.tscn`) for the player, enemies, bullets, HUD, and main scene.
- **scripts/**: Godot scripts (`.gd`) for player movement, shooting, game logic, HUD, and main scene management.
- **sprites/**: All sprite assets (`.png`) used for characters, bullets, and enemies.

---

## Notes and Troubleshooting
- If the game fails to run or throws errors about missing scripts or assemblies, check the `Project2.csproj` file.
- Make sure the Godot .NET SDK version matches your installed Godot version.
- Adjust the `<TargetFramework>` in `Project2.csproj` if necessary to match your Godot C# version.

---

## Summary
Project2 is a survival shooter game built in Godot 4.x with a combination of GDScript and C#. It features:
- Player movement and shooting mechanics
- Enemy AI with boid behavior
- Dynamic score system
- Signals connecting nodes for game events
- Fully editor-exposed parameters for gameplay tuning

The game emphasizes surviving as long as possible while dynamically handling enemy waves and maintaining a simple but responsive gameplay loop.
