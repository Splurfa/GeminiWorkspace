### **Stack Blueprint: The Sandbox Creation Engineer**

This document outlines the specific plan for the "Sandbox Creation Stack," the first implementation of the Prompt Engineer Architecture.

#### **1\. Mission & File Structure**

* **Mission:** To take a new application concept, from a simple idea to a detailed specification, and systematically generate a complete, actionable technical and design blueprint.  
* **Directory:** /stacks/sandbox/  
* **Managed by:** sandbox\_engineer.md. This is a dedicated AI instance whose system instructions are tailored specifically to orchestrate this three-prompt stack.

#### **2\. Execution Prompt Sequence**

This stack consists of three sequential prompts, copied from the Master Library into the local stack directory:

1. sandbox\_prompt\_34.md **(Pre-Code Planning Canvas):** Takes a core application idea and translates it into a structured project plan.  
2. sandbox\_prompt\_36.md **(Database Schema Designer):** Designs the database structure based on the project plan.  
3. sandbox\_prompt\_35.md **(Visual Design Direction Finder):** Creates the visual identity for the application.

#### **3\. Data Flow Map**

The sandbox\_engineer.md must be programmed with the following data flow logic to manage the sequence:

* **From \_prompt\_34 to \_prompt\_36:**  
  * The User Stories and Key Operations sections from the output of **\#34** are used as the primary input for **\#36**.  
* **From \_prompt\_34 to \_prompt\_35:**  
  * The Core Concept, Problem It Solves, and Target Audience sections from the output of **\#34** are used as the primary input for **\#35**.

#### **4\. System Configuration & Orchestration**

To run this stack, follow the standard multi-terminal orchestration cycle, beginning with the mandatory configuration check.  
**Step 0: System Configuration Check (In Orchestrator Terminal)**  
Before providing project context, the sandbox\_engineer must perform a configuration check:

1. **Acknowledge Builder Profile:** The Engineer first confirms its understanding of the user's profile.  
2. **Query for Environment Context:** The Engineer then asks for the critical platform-specific knowledge required for this stack (e.g., "What is the target database for this project?").  
3. **Ingest and Confirm:** Once the user provides the necessary information, the Engineer confirms the configuration and is ready to proceed.

**The Orchestration Cycle**

1. **Initiate:** Provide your project context to the sandbox\_engineer.md in Terminal 1\.  
2. **Step 1:** Use the Engineer to generate input for sandbox\_prompt\_34.md. Run this in Terminal 2\.  
3. **Feedback:** Paste the output from \#34 back into the Engineer. It will then generate the input for the next step.  
4. **Step 2:** Use the new input to run sandbox\_prompt\_36.md in Terminal 3\.  
5. **Continue:** Repeat the feedback loop for the final prompt in the stack.