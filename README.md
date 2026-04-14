# Cortex: The Alignment & Execution OS

An autonomous system that translates your high-level intent into the grueling work of dozens of specialized AI agents. You focus on the architectural vision; Cortex effortlessly compiles your thoughts into strict specifications, dispatches headless workers, and manages the Git state.

## The Three Layers of Hierarchical Intelligence

Cortex is built on a philosophy of strict separation of concerns, avoiding the "context collapse" that plagues open-ended AI coding agents. It mirrors a highly functional engineering organization across three layers:

### Layer 0: The Engine (The Subconscious)
*   **Repository**: [gemini-cli-headless](https://github.com/jarek108/gemini-cli-headless)
*   **Function**: Raw LLM API execution, subprocess routing, error handling, and JSON parsing. It knows nothing about your project or your intent. It is simply the resilient engine that powers the higher layers.

### Layer 1: The Execution Plane (The Factory Floor)
*   **Function**: Takes a specific, rigid machine contract (`IRQ.md`) and deterministically executes it. It manages the Git-Native State Machine, the Amnesia Engine, the Doer/QA loop, and The Glass Dashboard. It handles the "How."
*   *(See the detailed architecture of Layer 1 in the [Architecture Docs](docs/architecture/system_design.md))*

### Layer 2: The Alignment Plane (The Architect / The Boardroom)
*   **Function**: This layer focuses entirely on the "What" and the "Why." It is a continuous, evolving conversation with the human user (via the Manager persona). The goal is to build and refine the **Application Specification Document (ASD)**.
*   **The Workflow**: You never write Jira tickets or prompt the "Doer" agents directly. You talk to the Layer 2 Architect. The Architect updates the ASD, determines what components are needed, *autonomously* writes the Layer 1 contracts (`IRQ.md`, `QAR.md`), and dispatches the Layer 1 Factory Floor to build it. If Layer 1 hits a wall, it bubbles the error up to Layer 2, which translates it into a high-level architectural question for you.

---

## Why Cortex? Separating Alignment from Execution

The biggest failure mode of current "Agentic AI" (like AutoGPT) is trying to mash Layer 1 and Layer 2 into a single prompt. They try to figure out *what* you want while simultaneously trying to figure out *how* to write the regex to parse a specific file. This causes catastrophic context collapse and infinite loops.

By separating **Alignment (Layer 2)** from **Execution (Layer 1)**, Cortex protects the human from the noise of the terminal, and protects the execution agents from the ambiguity of human brainstorming. 

*   **To the human**, Cortex feels like a frictionless, conversational "vibe-code" interface. 
*   **To the agents**, Cortex feels like a brutal, deterministic factory floor governed by strict "Space-Grade Engineering Specifications."

## 📖 Documentation

Dive deeper into the philosophy and mechanics of the Cortex OS:

### Philosophy & Alignment (Layer 2)
*   [The Cortex Manifesto](docs/philosophy/manifesto.md)

### The Execution Engine (Layer 1)
*   [The Prompting Architecture](docs/architecture/prompting_architecture.md)
*   [System Design: Git as the State Machine](docs/architecture/system_design.md)
*   [The "Checkpoint" Concept (Time Travel)](docs/architecture/time_travel_and_checkpoints.md)
*   [The Artifact Contract & Reprimand Loops](docs/architecture/artifact_driven_flow.md)
*   [The Execution Lifecycle: Components & Artifacts](docs/architecture/execution_lifecycle.md)
*   [The Amnesia Engine & Context Injection](docs/architecture/amnesia_engine.md)
*   [Central Registry & Telemetry Management](docs/architecture/registry_and_state.md)
*   [Specialized QA & The Evolution of Skills](docs/architecture/specialized_qa_skills.md)
*   [The Glass: Observability Dashboard](docs/architecture/the_glass_dashboard.md)

### Usage
*   [Manager Toolbox (CLI Interaction)](docs/usage/manager_toolbox.md)
*   [Orchestrator Guide (E2E Workflows)](docs/usage/orchestrator_guide.md)

---

## Quick Start
*(Installation instructions pending physical split completion).*
