# Multi-Prompt Stack Blueprint

This document serves as the foundational guide for **designing, architecting, and strategically operating** multi-prompt stacks. It provides the conceptual framework for prompt engineers managing complex prompt sequences, ensuring modularity, efficiency, and effective orchestration within a human-in-the-loop execution model.

## 1. What is a Multi-Prompt Stack?

A multi-prompt stack is a sequence of interconnected prompts designed to achieve a complex, multi-stage outcome. Instead of a single, monolithic prompt, a stack breaks down a large task into smaller, manageable steps, each handled by a specialized prompt.

**Benefits:**
*   **Modularity:** Each prompt focuses on a single, well-defined task.
*   **Reusability:** Individual prompts can be reused across different stacks.
*   **Complexity Management:** Breaks down complex problems into simpler, sequential steps.
*   **Nuanced Results:** Allows for iterative refinement and transformation of information.
*   **Human-in-the-Loop Control:** Facilitates precise intervention and feedback at each stage.

## 2. The Prompt Engineer's Role in Stack Architecture

The prompt engineer (in this context, the AI agent, or you, if you are manually orchestrating) acts as the **architect and orchestrator** of the multi-prompt stack. This role involves more than just writing individual prompts; it's about designing the entire flow, ensuring seamless data transfer, and optimizing the stack's overall performance.

**Key Responsibilities:**
*   **Defining Stack Purpose:** Clearly articulating the complex problem the stack aims to solve and its desired final output.
*   **Designing Prompt Flow:** Mapping the sequence of prompts, including potential branching or iterative loops.
*   **Ensuring Data Integrity:** Specifying how output from one prompt becomes input for the next, ensuring data consistency and format compatibility.
*   **Optimizing Performance:** Identifying bottlenecks, refining individual prompts, and adjusting the sequence for efficiency and quality.
*   **Maintaining Stack Integrity:** Regularly reviewing and updating the stack to adapt to new requirements or improved prompt engineering techniques.

## 3. Core Architectural Principles for Stacks

This blueprint leverages the principles outlined in the `[[prompt-engineer-architecture]]` document, applying them specifically to the design and interconnection of prompts within a stack.

*   **Modularity:** Each prompt within a stack should be a self-contained unit, performing a single, well-defined function. This allows for easier testing, debugging, and reuse.
*   **Clear Input/Output Contracts:** Define precise expectations for each prompt's input and output. This is crucial for ensuring smooth data flow between sequential prompts.
*   **Data Flow & Transformation:** Design how information flows and transforms from one prompt's output to the next prompt's input. This often involves specifying which sections of an output become the primary input for the subsequent prompt.
*   **Error Handling & Resilience:** Consider how the stack will handle unexpected outputs or errors from individual prompts. While not always explicitly coded, the design should account for potential deviations.
*   **Orchestration Patterns:** Recognize common stack patterns (e.g., linear sequence, conditional branching, iterative loops) and choose the most appropriate pattern for the task.

## 4. Operational Framework for Stacks: The Human-in-the-Loop Execution Model

The `[[prompt-assembly-protocol]]` provides the detailed steps for building and testing individual prompts. This blueprint focuses on how those steps fit into the larger operational cycle of a multi-prompt stack, emphasizing the **human-in-the-loop orchestration** that drives execution in this environment.

**Understanding Stack Execution:**

Unlike fully automated scripts, running a multi-prompt stack in this Gemini CLI environment involves a collaborative process between the user and the AI agent (me). The actual executable logic for a specific stack resides in its dedicated `engineer.md` file.

**The Role of the `engineer.md` File:**
*   Each specific multi-prompt stack (e.g., the `sandbox` stack) has an `engineer.md` file located within its stack directory (e.g., `10_stacks/sandbox/engineer.md`).
*   This `engineer.md` file contains the **specific instructions, prompt sequence, and data flow logic** that the AI agent (me) follows to orchestrate that particular stack. It is the "executable blueprint" for that stack.
*   It defines the mission, the prompts involved, how data moves between them, and the interaction points with the user.

**Stack Lifecycle Phases (Human-in-the-Loop Perspective):**

*   **Design & Prototyping:**
    *   **Objective:** Conceptualize the stack, define its overall purpose, and identify the necessary stages or transformations.
    *   **Action:** Select or design the individual prompts required for each stage, considering their input/output contracts. Draft the `engineer.md` file for the stack.
*   **Assembly & Integration:**
    *   **Objective:** Build and connect the individual prompts into a cohesive sequence.
    *   **Action:** Copy prompts to the local stack folder (as per `Prompt Engineer Architecture`), and define the data flow logic within the `engineer.md` file that dictates how outputs feed into subsequent inputs.
*   **Testing & Validation:**
    *   **Objective:** Evaluate the stack's end-to-end performance and the quality of its final output.
    *   **Action:** The user initiates the stack by instructing the AI agent (me) to "run" or "execute" the stack (referencing its `engineer.md` file). The AI agent then guides the user through the sequence, generating prompt inputs, and waiting for user execution and output feedback.
*   **Deployment & Monitoring:**
    *   **Objective:** Put the stack into regular use and observe its behavior in real-world scenarios.
    *   **Action:** Implement the stack within your workflow, and monitor its outputs for consistency and effectiveness, providing feedback to the AI agent as needed.
*   **Iteration & Refinement:**
    *   **Objective:** Continuously improve the stack based on performance data, new requirements, or evolving prompt engineering techniques.
    *   **Action:** Adjust prompt designs, modify data flow logic within the `engineer.md` file, or re-sequence prompts as needed.

## 5. Stack-Specific Implementations

This blueprint provides a general framework. Individual stacks (e.g., the sandbox stack) will have their own dedicated documentation that details their specific prompt sequences, configurations, and operational nuances. These documents (typically `engineer.md` files within the stack's directory) serve as concrete *implementations* of this general blueprint.

**Example:** The `10_stacks/sandbox/engineer.md` file is a specific implementation. Its content details the mission, prompt sequence, and data flow for the sandbox stack, adhering to the principles outlined in this blueprint.

## 6. Adherence to System Protocols

All stack-related documentation, including this blueprint and specific stack implementation files (e.g., `engineer.md`), must adhere to relevant system-wide guidelines. This ensures consistency and discoverability across your entire knowledge base.

## 7. Relationship to Project-Specific Prompts

This blueprint describes the architecture for complex, multi-stage prompt workflows (stacks). For simpler, individual prompts that are specific to a particular project and are not part of a multi-step orchestrated sequence, please refer to the `_prompts` sub-folder structure defined in the [[project-manifest-protocol]].

*   **Multi-Prompt Stacks:** Designed for automated or semi-automated execution of a sequence of prompts to achieve a complex outcome. Prompts are copied into a local stack folder and orchestrated by an `engineer.md` file.
*   **Project-Specific Prompts:** Designed for individual, standalone prompts that are relevant to a specific project. These are stored in the project's `_prompts` sub-folder and are typically executed manually or as single-shot operations.
