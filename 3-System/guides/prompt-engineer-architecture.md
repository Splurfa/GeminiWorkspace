### **Framework: The Prompt Engineer Architecture**

This document outlines the general architecture for creating modular, sequential prompt stacks. Each stack is managed by its own dedicated "Prompt Engineer," a specialized AI instance that orchestrates a series of "Execution Tool" prompts to accomplish a complex task.

#### **1. System Architecture: A Two-Tiered Model**

Any stack built using this framework is composed of two distinct tiers that work together:

* **Tier 1: The Prompt Engineer (Orchestrator)**  
  * **Description:** A dedicated AI instance for a specific stack, running in its own persistent terminal window within the Gemini CLI environment.  
  * **Role:** Acts as the "architect" or "orchestrator." Its primary function is to process the user's context and manage the data flow between the steps in its sequence.  
* **Tier 2: The Prompt Stack (Execution Tools)**  
  * **Description:** The individual prompts that make up a stack. Each prompt is run in its own, separate terminal window.  
  * **Role:** Acts as a specialized "tool" that performs one specific task within the sequence.

#### **2. File System & Naming Conventions**

To ensure AI coherence and system modularity, a specific file structure is required. This creates a "contextual scope" for each stack.

* **Master Prompt Library:** A central repository located at [[00-master-prompt-library]] containing all 41 Essential Prompts. This serves as the "source of truth" and reference knowledge.  
* **Local Stack Folders:** For each new stack, a dedicated directory is created (e.g., /stacks/sandbox/).  
  * **Engineer File:** The instructions for the orchestrator are stored in a file named using the convention: \[stack\_name\]\_engineer.md (e.g., sandbox\_engineer.md).  
  * **Prompt Files:** The specific prompts needed for the stack are *copied* from the Master Library into this local folder and named using the convention: \[stack\_name\]\_prompt\_\[number\].md (e.g., sandbox\_prompt\_34.md).

This structure ensures that each Engineer only references the "tools on its belt" within its local folder, preventing context bloat and confusion.

#### **3. Core Engine Design (For Any Prompt Engineer)**

Each Prompt Engineer instance should be built with the following components:

* **Knowledge Base:** The engine's primary intelligence should come from a dedicated knowledge base populated with the complete library of **Nate Jones's Prompt Engineering Techniques**.  
*   **System Instructions:** The engine receives a unique set of system instructions that defines its specific role and the stack it manages. These system instructions *must* incorporate the foundational principles and framework of `[[07-prompt-improver]]` (Prompt #7 from the Master Prompt Library) as their core, ensuring a consistent and proven methodology for prompt construction and refinement.
* **Sequential Chaining & Data Handling Logic:** The engine's instructions must include a simple, internal map for its prompt sequence, knowing which output fields from one prompt become the inputs for the next.

#### **4. Operational Workflow: The Orchestration Cycle**

This system is designed for a precise, "human-in-the-loop" orchestration process managed by the user across multiple terminals.

1. **Initiation:** Activate the specific **Prompt Engineer** (e.g., sandbox\_engineer.md) in its own terminal.  
2. **Configuration Check:** The Engineer runs its mandatory configuration check to calibrate itself to the user and tech stack.  
3. **Generate & Execute:** The Engineer generates input for the first prompt in its local folder (e.g., sandbox\_prompt\_34.md). The user runs this in a new terminal.  
4. **Feedback Loop:** The user pastes the output from the execution terminal back into the Engineer's terminal.  
5. **Continue Cycle:** The Engineer processes the output and generates the input for the next prompt in its sequence. The user repeats the process until the stack is complete.

#### **5. Relationship to Project-Specific Prompts**

This architecture describes the framework for complex, multi-stage prompt workflows (stacks) orchestrated by a dedicated Prompt Engineer. For simpler, individual prompts that are specific to a particular project and are not part of a multi-step orchestrated sequence, please refer to the `_prompts` sub-folder structure defined in the [[project-manifest-protocol]].

*   **Prompt Engineer Architecture:** Designed for automated or semi-automated execution of a sequence of prompts to achieve a complex outcome. Prompts are copied into a local stack folder and orchestrated by an `engineer.md` file.
*   **Project-Specific Prompts:** Designed for individual, standalone prompts that are relevant to a specific project. These are stored in the project's `_prompts` sub-folder and are typically executed manually or as single-shot operations.