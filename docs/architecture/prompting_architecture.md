# The Prompting Architecture

The current trend in "AI coding" is to constantly tweak custom prompts for every new task. This causes prompt explosion and forces you to micromanage agents instead of engineering software.

To solve this, Cortex abandons custom prompt engineering entirely. Instead, we use a rigid, distributed prompting stack divided into three parts:

1. **Role Prompts:** Who the agents are and what authority they have (OS Kernel).
2. **Artifact Templates:** How the agents communicate and transition states (Universal API).
3. **Project Knowledge:** The specific technical rules and testing rituals for your codebase (Project Brain).

---

## Role Prompts & The Layered Hierarchy
*Location: Workspace Root (`GEMINI.md`) for Layer 2, Orchestrator Source (`templates/roles/`) for Layer 1 modes.*  

We restrict the system to exactly **three universal agent roles** distributed across two cognitive layers. 

### Layer 2: The Alignment Plane (The Manager / Architect)
The Manager sits between the human and the execution plane. It operates strictly in the realm of Intent and Specification:
*   **The Boardroom (Interactive)**: The CLI agent you talk to. It does not write code. It asks sharp questions, probes edge cases, and helps you refine the **Application Specification Document (ASD)**. It seeks to reach a "Certainty Threshold" regarding your intent.
*   **The Desk Work (Headless)**: Once certainty is reached, the Manager goes offline. In this headless mode, it acts as a bureaucratic clerk, parsing the ASD and your conversation into rigid, Space-Grade Engineering Specifications (`IRQ.md` and `QAR.md`) for the Factory Floor.

### Layer 1: The Execution Plane (The Factory Floor)
The Factory Floor does not care about the "Why"; it only cares about the "How".
*   **The Doer (The Builder)**: The blind builder. It reads the tasks (`IRQ.md`) and project rules, writes the code, and produces an Implementation Report (`IRP.md`). It is explicitly forbidden from expanding scope or questioning the architecture.
*   **The QA (The Enforcer)**: The strict enforcer. It reads the QA Request (`QAR.md`) and project rules, blindly executes the required tests, and produces a QA Report (`QRP.md`). It rejects the work if any rule is broken.

---

## Artifact Templates
*Location: Orchestrator Source (`templates/artifacts/`)*  

We don't rely on chat messages to know if a job is done. Agents must structure their thoughts and outputs using strict Markdown templates. These artifacts act as the compiled interface between Layer 2 and Layer 1, and serve as "Black Box Flight Recorders" if the system crashes.

*   **Implementation Request (IRQ):** The Manager's compiled contract telling the Doer what to build and what not to touch.
*   **QA Request (QAR):** The Manager's compiled contract telling the QA what specific risk areas to test.
*   **Implementation Report (IRP):** The Doer's receipt proving it finished the work and noting any edge cases.
*   **QA Report (QRP):** The QA's final verdict (`final` or `to correct`) including accumulated historical feedback for the Amnesia Engine.

---

## Project Knowledge
*Location: Target Workspace (`projects/my-app/GEMINI.md`, `designs/`)*  

This is where **100% of the project specificity lives**. When the generic Doer and QA agents wake up, they read this layer to understand your tech stack, architectural rules, and testing rituals. 

Crucially, **Project Knowledge is a learning system managed by Layer 2.**

### The Skill Growth Lifecycle:
Instead of rewriting agent prompts when a mistake happens, the system learns like a real engineering team:

1. **The Failure:** The Doer and QA finish a task, but you notice a UI element overlaps on mobile screens. 
2. **The Intervention:** You tell the Manager CLI: *"You both missed the UI overlap on the mobile viewport."*
3. **Policy Formulation:** The Manager autonomously updates your project's `GEMINI.md` file, adding a new rule under `## QA Rituals`: *"Mobile Viewport Check: QA must run `mobile_test.sh`."*
4. **Permanent Hardening:** The system has permanently learned. The next time the QA agent boots up for a UI task, it reads the updated Project Knowledge and ruthlessly enforces the new mobile test.