**Coding Standards & Best Practices**

# Purpose

These coding standards establish a consistent approach to writing, organizing, and maintaining code for Pestila.

All six developers are expected to follow these standards so that code can be understood, modified, evaluated, and maintained by any member of the team.

These standards are also applicable to code created or modified with generative AI.

# 1. General Principles

Code should prioritize:

- Readability
- Consistency
- Maintainability
- Simplicity
- Reusability
- Separation of responsibilities
- Minimal coupling between systems
- Reasonable performance
- Team compatibility

We as developers should now start to avoid treating our work that we do as “my code.” Once code that we implement into the project, it now has become the team’s code for this project.

---
# 2. Project Organization

Unity assets should be placed into consistently named folders.

Example Project Structure:

Assets

             Arts

            - Characters

            - Enemies

            - Environment

            - UI

            - VFX

            Audio

            - Music

            - SFX

            Materials

            Prefabs

            - Player

            - Enemies

            - Environment

            - Mutations

            -UI

            Scenes

            - Levels

            - Menus

            - Testing

            Scripts

            - Core

            - Player

            - Combat

            - Enemies

            - Mutations

            - UI

            - Managers

# 3. Naming Conventions

***Classes**

Use PascalCase:

Public class PlayerMovement : MonoBehavior

{
}

Public class EnemyController : MonoBehavior

{
}

Public class MutationManager : MonoBehavior

{
}

Avoid using names like:

Public class pl_mov

{
}

Public class enemyctrl

{
}

*Methods***

Use PascalCase:

HandleMovement();

PerformAttack();

TakeDamage();

Apply Mutation();

ResetRun();

Avoid using names like:

DoThing();

Process();

HandleStuff();

***Variables**

Use **camelCase**:

Private float movementSpeed;

Private int currentHealth;

Private float attackCooldown;

Private bool isGrounded;

Avoid using names like:

Float s;

Int x;

Bool thing;

****Boolean Variables**

Use names that clearly indicate a true/false condition:

bool isDead;

bool canAttack;

bool hasMutation;

bool isBossActive;

Avoid using names like:

bool check;

bool value;

bool state;

***Script Files**

A C# script filename should match the primary class contained within the file.  
For example:  
PlayerMovement.cs

 public class PlayerMovement  :  MonoBehavior

{

}

---

# 4. Code Organization

Each class should have one clear responsibility so that systems are easier to understand, evaluate, and modify.

PlayerMovement – Manages player movement and sprinting.

PlayerCombat – Manages basic attacks and combat actions.

PlayerHealth – Manages player health, damage, and death.

PlayerAbility – Manages class-specific abilities.

EnemyController – Manages enemy behavior and decision making.

EnemyHealth – Manages enemy health and death.

MutationManager – Manages mutations and upgrades during a run.

RunManager – Manages run progression, restarting, and win/loss states.

BossController – Manages boss-specific behavior.

UIManager – Manages gameplay UI updates.

OptionsMenuUI – Manages options menu interactions.

# 5. Inspector Variables

Variables that need to be adjusted through the Unity Inspector should normally use [SerializeField].

Avoid making a varuable public only so that it appears in the Inspector.

Avoid:

Public float movementSpeed = 5.0f;

Preferred:

[SerializeField] private float movementSpeed = 5.0f;

This keeps outside scripts from changing values unnecessarily.

---

# 6. Methods Should Have Clear Responsibilities

Methods should normally perform one clearly defined task.  
For example, a player script from a research prototype could begin as:

Private void Update ()

{

              Float horizontal = Input.GetAxis(“Horizontal”);

              Float vertical = Input.GetAxis(“Vertical”);

              // Movement code

              // Sprint code

              // Attack code

              // Ability code

}

As the system continues to grow, responsibilities should be separated:

Private void Update();

{

              HandleMovement();

              HandleSprint();

              HandleCombatInput();

}

Then:

Private void HandleMovement()

{

    // Player movement logic

}

Private void HandleSprint()

{

    // Sprint logic

}

Private void HandleCombatInput()

{

    // Combat input logic

}

# 7. Comments

Code should be understandable primarily through descriptive names.

Comments should explain why something is being done when the reason may not be immediately obvious.

Avoid comments that simply repeat the code.

Bad:

// Set speed to sprint speed.

currentSpeed = sprintSpeed;

The code already explains this.

A more useful comment would be:

// Prevent sprinting while the player is performing an attack.

if (isAttacking)

{

    currentSpeed = movementSpeed;

}

Comments can also explain unusual behavior discovered during testing.

// Apply movement after gravity calculation so CharacterController

// remains grounded correctly while moving down slopes.

controller.Move(movement * Time.deltaTime);

**TODO Comments**

Use TODO for known unfinished functionality.

// TODO: Replace temporary projectile with final class ability.

// TODO: Add final boss attack animation.

TODO comments should eventually be completed or removed.

---

# 8. Unity Practices

Unity lifecycle methods should be used for their intended purposes.

Awake(): Use it for references or initializations needed immediately when the object loads.

Private void Awake()

{

              Controller = GetComponent<CharacterController>();

}

Start(): Use it for setup that happens before normal gameplay begins.

Private void Start()

{

              currentHealth = maxHealth;

}

Update(): Use it for frame-based gameplay and input.

Private void Update()

{

              HandleMovement();

HandleCombatInput();

}

FixedUpdate(): Use it for when working with physics system that depends on Unity’s physics timestep.

Developers should avoid putting every system into Update() simply because it runs continuously.  
  

# 9. Keep Changes Focused

When working on a feature, developers should avoid unnecessarily modifying unrelated systems.

For example, someone implementing enemy pathfinding should not reorganize the player's combat code unless the task specifically requires it.

Focused changes make code reviews, debugging, and Git merges easier.

---

# 10. Reuse Existing Systems

Before creating a new script or system, developers should determine whether the project already contains something that performs the same responsibility.

For example, if a health component already exists:

PlayerHealth

A developer should not create:

NewHealthSystem

Simply because they prefer a different implementation.

The existing system should be extended when reasonable.

Major replacements should be discussed with the team first.

# 11. Keep Code Simple

Pestila has a limited development schedule, so development should focus on completing the game's core functionality.

Prefer:

A simple system that works reliably

Not Preferred:

A complex system that the team cannot finish or maintain.

Developers should avoid adding:

-          Frameworks.

-          Third-party packages.

-          Complicated inheritance structures.

-          Unneeded managers.

-          Advanced optimization systems.

-          Design patterns with no clear benefit.

Systems should become more complex only when the project requires that complexity.

# 12. Generative AI

Generative AI may be used as a learning and research tool but may not be used to create or develop the project's code, systems, or other required deliverables.  
AI may be used to:

- Research Unity systems, programming concepts, and development methods.
- Ask questions about how a system or programming concept works.
- Explore different approaches to solving a programming problem.
- Function as a "rubber duck" to discuss, analyze, or troubleshoot code that the student has written.
- Help identify probable causes of an error or unexpected behavior.
- Explain unfamiliar code, terminology, or documentation.  
    AI should not be used to:
- Generate code or systems for the project for the student to incorporate.
- Rewrite or modify project code.
- Generate complete scripts, features, mechanics, or other required project functionality.
- Generate project documentation or other deliverables that are expected to demonstrate the student's own work.
- Replace the student's own research, problem solving, or understanding of the systems being developed.

# Student Responsibility

AI may only be used to support learning, not replace the development process. Students are responsible for writing, implementing, evaluating, and understanding their own project.  
Students should be able to explain the code and systems they create, including:

- How the system works.
- What data structures or important variables are being used and why.
- Why is the chosen approach appropriate for the problem?
- How the system interacts with other parts of the project.  
    AI assistance should help a student learn how to solve a problem, not provide the solution that the student submits.

---