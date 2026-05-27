Idea 1: "The Adaptive Combat Arena" 
The Goal: Test basic local gameplay logic, interface binding, performance profiling, and behavior rules.  
How the Team Must Co-operate:
Tolani: Programs a basic third-person character in C++ who can perform two distinct types of attack: a regular strike and a heavy magic ability.  
Majid: Builds a modular floating health bar HUD in UMG that tracks both the player’s health and the target enemy's health in real-time.  
Abdullah: Sets up a simple training dummy utilizing an Unreal AI Behavior Tree. He configures a rule: if the dummy takes heavy magic damage 3 times in a row, its tree changes states to activate an "Immunity Shield". 
Praise: Acts as the environment and performance coordinator. He configures the repository workflow via GitHub/Git LFS, merges everyone's work branches, and runs Unreal's built-in profiling tools to verify that the combat loop runs at a flawless 60fps baseline

Idea 2: "The Cross-Era Vault System"
The Goal: Test external database persistence, cloud/API networks, player save systems, and variable-driven interface shifts .  How the Team Must Co-operate:
Praise: Deploys a functional local instance of a PostgreSQL or MongoDB database and creates a lightweight Node.js/Python API that exposes a secure endpoint to save/load player stats .  
Tolani: Programs an interactive volume box in Unreal ("The Portal Box"). When the player steps inside it and clicks an input, it triggers an event that gathers the character's inventory data array and pushes it to Praise's API.  
Majid: Designs a dynamic inventory menu screen. He programs it so that if the character variables state they are currently in a "Prehistoric Era," the menu frame draws a simple wood aesthetic; if changed to a "Cyberpunk" flag, the border updates to a neon style.  
Abdullah: Focuses on test planning and edge-case validation. He creates the data blueprint layout inside Notion for item IDs. He then purposely attempts to break the project by forcing bad save calls (e.g., losing connection mid-portal) to check if player data corrupts. 

Idea 3: "The Multiplayer Replication Sync"
The Goal: Test dedicated server connections, multi-client position synchronization, combat replication, and layout scaling .  How the Team Must Co-operate:
Praise: Configures a dedicated server build environment inside Unreal, enabling multi-user network connections.  
Tolani: Adjusts the primary character class to support native Actor Replication and RPCs . He ensures that when a player triggers an action, the rotation vectors and animation flags mirror safely across to all other connected clients.  
Majid: Creates a multiplayer lobby UI frame and a chat log component in UMG, making sure the design uses responsive parameters that dynamically scale across completely different display screen sizes.  
Abdullah: Coordinates a structured network stress-test log. He runs two separate standalone instances of the build, simulates network latency/packet loss variables, and records whenever player positions stutter or inputs fail to register across screens.

Idea 4: "The UGC Engine Architecture"
The Goal: Test data-driven engineering practices, Unreal Data Tables, custom narrative scripts, and tool setups.  How the Team Must Co-operate:
Abdullah: Designs a detailed quest template document inside Notion that standardizes how a community player submits a storyline. He builds out a branching narrative loop in Twine to demonstrate how choices impact basic values.  
Majid: Takes Abdullah's logic properties and maps them out inside an Unreal Data Table layout, configuring data definitions for QuestID, RequiredEra, and RewardAmount.  
Tolani: Writes a flexible Blueprint/C++ manager subsystem that opens that data table, cycles through the rows, and dynamically builds an in-game quest acceptance box based on whatever information was typed into the spreadsheet lines.  Praise: Builds an automated pipeline checking tool. He creates an engine script validating that if any team member accidentally appends corrupt characters or missing values to the text fields inside the Data Tables, the project fails to package cleanly, printing out specific warnings before logging it onto their shared Notion hub.


