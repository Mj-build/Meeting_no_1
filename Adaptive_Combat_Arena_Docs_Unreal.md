**Adaptive Combat Arena**

*Mini Prototype — Team Documentation & Game Design Write-Up*

Version 1.0  |  Team Project


**1. Project Overview**

The Adaptive Combat Arena is a 3D mini prototype built to test core local gameplay logic, interface binding, performance profiling, and behavior rules.

The prototype features a third-person character facing off against an AI-driven training dummy in a simple combat loop, demonstrating attack mechanics, health tracking, and a clean HUD — all built natively using C++ and Unreal Engine, managed via a structured source-control pipeline.

This document covers:

* The game design specification for the prototype
* Each team member's assigned responsibilities
* How the four contributors must co-operate to deliver the build
* Technical notes and acceptance criteria
**2. Game Design Write-Up**

**2.1 Concept**

A playable third-person character and a stationary target dummy are placed in a local combat arena.

The player controls the character and can trigger two distinct types of attack against the dummy. The game loop evaluates real-time damage and tracks health. The UI interface must display both characters' health states and target tracking at all times.

**2.2 Characters**


| Attribute | Playable Character | Training Dummy |
| --- | --- | --- |
| Type | C++ Third-Person Character | AI-driven Actor |
| Starting HP | 100 | 100 |
| Role | Controlled by player | Stationary target with behavior rules |
| Control System | Player Input Actions | Unreal AI Behavior Tree |


**2.3 Attack Mechanics**

The player character features two distinct attack options programmed in C++:

* Regular Strike: Deals -10 HP to the training dummy.
* Heavy Magic Ability: Deals -20 HP to the training dummy.
On each attack execution, the character performs the corresponding attack capability. The target dummy's health updates immediately in real-time after the hit registers.

**2.4 Health Bar Rules**

* A modular floating health bar HUD tracks both the player's health and the target enemy's health in real-time.
* Health bars decrease smoothly via UI material/parameter interpolation when damage is applied.
* Health values are displayed numerically alongside the bar (e.g., 80 / 100).
* When a character reaches 0 HP, the system updates the game state to handle defeat.
* Health values are clamped and cannot drop below 0.
**2.5 Win & Behavior Condition**

* The target dummy utilizes an Unreal AI Behavior Tree to evaluate hits.


| Behavior Rule: If the dummy takes heavy magic damage 3 times in a row, its behavior tree changes states to activate an "Immunity Shield". |
| --- |

The dummy is defeated when its HP reaches zero, triggering the win state and an option to reset the arena.

**2.6 Arena & Visual Style**

* A localized, clean environment setup optimized for performance profiling.
* The floating HUD components track above the characters in 3D space or screen space.
* Combat animations and hit impacts are visually distinct depending on whether a regular strike or a heavy magic ability is used.
**2.7 Tech Stack**

* C++ — Core character classes, input handling, and base gameplay systems.
* Unreal Engine — Core game engine and runtime environment.
* UMG (Unreal Motion Graphics) — UI/HUD architecture and real-time health tracking elements.
* AI Behavior Trees — System driving the target dummy's logic, hit tracking, and conditional states.
* Built-in Profiling Tools — Monitoring tools (e.g., Unreal Insights, stat commands) used to ensure a consistent performance baseline.
* GitHub & Git LFS (Large File Storage) — Version control platform and large-asset management extension for tracking project binaries, blueprints, and code changes cleanly.
**3. Team Roles & Responsibilities**

The four team members each own a distinct vertical of the prototype. Work is divided so that each person can build and test their slice independently before the final integration.

**3.1 Tolani — Character Logic & Attack System**

Tolani is responsible for programming the core gameplay behavior of the third-person character and the attack interactions in C++.

***Deliverables***

* A custom C++ Character class with attributes for health management (CurrentHP, MaxHP) and character state.
* Core attack functions executing either a regular strike or a heavy magic ability.
* Logic to apply damage to targets, reducing health by 10 for regular attacks and 20 for heavy magic attacks.
* Health clamping functions ensuring remaining health never drops below 0.
* Exposed functions and delegates (UPROPERTY / BlueprintAssignable) so Majid's HUD and Praise's integration hooks can bind cleanly.
***Acceptance Criteria***

* Triggering a regular strike reduces the target's HP by exactly 10.
* Triggering a heavy magic ability reduces the target's HP by exactly 20.
* Health values clamp perfectly at 0 and never go negative.
* Actors correctly initialize with 100 HP on match start.
**3.2 Majid — Health Bar HUD**

Majid builds the modular floating health bar HUD in UMG that tracks and displays health states in real-time.

***Deliverables***

* Modular UMG health bar widgets configured for screen space or world space tracking.
* Dynamic UI elements showcasing a color-filled progress bar scaling with HP percentage, alongside a numeric readout (e.g., 80 / 100).
* Event-driven UI updates linked to Tolani's C++ damage delegates to refresh health bars instantly upon impact.
* Smooth visual transitions on the health bar fill when damage is registered.
* A visually distinct zero-HP state indicating defeat (e.g., bar turns gray or red).
***Acceptance Criteria***

* Both health bars display and initialize accurately on level load (100/100).
* Bar fill percentage and numerical metrics update accurately after each registered hit.
* Visual interpolation plays smoothly on every health change.
* The zero-health state is immediately distinguishable from active states.
**3.3 Abdullah — Training Dummy & Behavior Tree**

Abdullah sets up the simple training dummy actor and configures its adaptive behavior rules utilizing an Unreal AI Behavior Tree.

***Deliverables***

* A training dummy actor placed within the level layout acting as a stationary combat target.
* An AI Controller and Behavior Tree asset managing the dummy's conditional logic states.
* A tracking counter within the behavior tree/blackboard to monitor heavy magic hits.
* State Rule: A conditional branch or decorator that activates an "Immunity Shield" state automatically if the dummy takes heavy magic damage 3 times in a row.
***Acceptance Criteria***

* The dummy tracks incoming damage types properly within its AI architecture.
* Taking 3 heavy magic abilities consecutively triggers the "Immunity Shield" state change in the behavior tree.
* Regular strikes do not increment or trigger the immunity shield condition.
* The dummy resets its internal counter and state cleanly when a new round is initialized.
**3.4 Praise — Integration, Performance & Build Co-ordination**

Praise acts as the environment and performance coordinator. He wires the systems together, configures the repository workflow, and runs performance validation.

***Deliverables***

* System integration: binding character inputs, delegates, UI instances, and AI components into a cohesive loop.
* Repository architecture setup via GitHub, utilizing Git LFS to handle large assets (maps, meshes, animations) efficiently.
* Branch management: maintaining a clean branching workflow, merging feature branches, and resolving conflicts.
* Performance validation using Unreal Engine's built-in profiling tools to verify that the combat loop runs at a flawless 60fps baseline.
* A global state manager handling match reset capabilities, restoring actor health and resetting AI behavior trees.
***Acceptance Criteria***

* The entire combat loop triggers seamlessly end-to-end without functional breaks or unhandled dependencies.
* The game state manager successfully handles win conditions and complete match resets.
* Profiling passes confirm stable performance matching or exceeding the 60fps target baseline.
* All team branches are integrated into the main repository branch with a clean, conflict-free commit history.
**4. Team Co-operation Workflow**

**4.1 Branch Strategy**

Each member works entirely within their assigned feature branch on GitHub to protect code stability. Direct commits to the main branch are restricted.

* feature/tolani — Character C++ classes and core damage logic.
* feature/majid — UMG health bar HUD layouts and bindings.
* feature/abdullah — Training dummy setup, AI Controllers, and Behavior Trees.
* Praise operates on integration pipelines and manages final merges to the main branch.
**4.2 Integration Order**

To prevent structural blockages, the development workflow follows a strict sequential pipeline:

* 1. Tolani establishes and pushes the foundational C++ classes and data structures first, ensuring an accessible API.
* 2. Majid pulls Tolani's completed code branch to bind the UMG interfaces directly to the newly exposed health delegates.
* 3. Abdullah designs the training dummy and AI Behavior Tree logic in parallel, ensuring compatibility with the base damage structures.
* 4. Praise executes the final merge of all three functional branches using GitHub/Git LFS, hooks up global input events, and initializes profiling sweeps.
**4.3 Communication Checkpoints**

* Daily Status: Team members provide brief, one-line updates in the shared channel (Completed / Blocked / Active).
* API Availability: Tolani notifies the team immediately when the C++ damage and character hooks are compiled and live, enabling Majid and Abdullah to pull changes.
* Peer Reviews: Merge requests require a review from at least one peer before Praise performs final validation and pushes to the main branch.
**4.4 Definition of Done**

* All feature-specific acceptance criteria listed in Section 3 pass inspection.
* The project compiles and runs within Unreal Engine smoothly without log errors or crashes.
* Performance metrics consistently satisfy the 60fps baseline during profiling.
* All branches are combined into the main branch with a clean Git LFS asset history.
**5. Summary — Who Does What**


| Member | Core Responsibility | Key Output | Integration Point |
| --- | --- | --- | --- |
| Tolani | Character logic & attack architecture | C++ Character class & damage events | Bound to inputs and UI delegates |
| Majid | Health bar HUD | Modular UMG widgets | Binds to character health updates |
| Abdullah | Dummy logic & AI rules | Behavior Tree & "Immunity Shield" | Evaluates incoming damage properties |
| Praise | Workflow, profiling & integration | Git LFS repo, state manager, profiling logs | Validates performance baseline (60fps) |


