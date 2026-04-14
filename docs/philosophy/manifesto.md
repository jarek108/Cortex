# The Cortex Manifesto

## The Promise vs. The Reality

For years, the promise of "agentic AI" was simple: you tell an AI to build a feature, you sit back, and it writes the code. 

But if you've actually used these tools on a real project, you know the reality is different. When an AI is given free rein over your codebase, it gets easily distracted. It encounters a minor bug and decides to rewrite three unrelated files just to "fix" it. It ignores your architectural rules. 

Your job degrades from being an *engineer* to being a *babysitter*. You spend hours reviewing massive, confusing code changes, trying to figure out what the AI actually did. This isn't saving you time—it's just replacing the stress of writing code with the stress of supervising an unpredictable intern.

*(For a technical breakdown of why this happens, see [The Terminal Babysitting Trap](the_terminal_babysitting_trap.md)).*

## The Strategic Pivot: Hierarchical Intelligence

The biggest failure mode of current "Agentic AI" (like AutoGPT or Devin) is attempting to mash two entirely different cognitive processes into a single prompt. They try to figure out *what* you want (Alignment) while simultaneously trying to figure out *how* to write the regex to parse a specific file (Execution). This causes catastrophic context collapse and infinite loops.

To make an autonomous agent truly useful in a production environment, you must separate **Alignment** from **Execution**. We built **Cortex** to mirror the structure of a highly functional engineering organization, dividing labor across three distinct layers:

### Layer 0: The Engine (The Subconscious)
The raw API execution layer (`gemini-cli-headless`). It handles network retries, JSON parsing, and basic CLI interactions. It knows nothing about your project; it simply provides raw cognitive horsepower.

### Layer 1: The Execution Plane (The Factory Floor)
This layer takes a specific, rigid machine contract (`IRQ.md`) and deterministically executes it. It manages the Git-Native State Machine, the Amnesia Engine, and the brutal Doer/QA loop. It does not think about architecture; it only thinks about *How* to fulfill the contract.

### Layer 2: The Alignment Plane (The Architect / Cortex)
This is where you, the human, interact with the system. This layer focuses entirely on the "What" and the "Why." 

You never write Jira tickets or prompt the "Doer" agents directly. You engage in a continuous, evolving conversation with the Layer 2 Architect to refine an **Application Specification Document (ASD)**. 

## The Illusion of 1-to-1, The Reality of 1-to-Many

**To the human**, Cortex feels like a frictionless, conversational "vibe-code" interface. It feels like you are pair-programming with a single, highly aligned Senior Architect. You discuss the vision, and your intent effortlessly flows into the system.

**To the agents**, Cortex is a massive, grueling engine of execution. The moment your intent crosses the "Certainty Threshold" in the Boardroom, Cortex silently fractures your thought into dozens of highly specific, machine-readable contracts. It spawns a legion of blind "Doers" to hammer out the code, and a squad of ruthless "QA" agents to test it against your project's invariants. 

You experience the effortless flow of pure intention. The agents experience the grueling reality of software engineering.

## Core Principles of the Factory Floor (Layer 1)

While you interact with Layer 2, Layer 1 enforces the following hard rules behind the scenes:

1. **Isolation is Mandatory**: An execution agent operates in a sandboxed Git branch, unaware of the control plane orchestrating it.
2. **Artifact-Driven State (The Flight Recorders)**: Conversation history is volatile and prone to LLM drift. State must be externalized. Agents communicate progress exclusively through strictly formatted Markdown files generated on the physical disk. These artifacts act as "Black Box Flight Recorders"—audit logs for the system rather than input fields for humans.
3. **Engineered Amnesia**: LLMs suffer from severe "anchoring bias." The OS enforces session amnesia, wiping the agent's memory and strategically injecting only the most relevant historical feedback via XML before each run.
4. **Deterministic Routing**: The system parses the literal `[STATUS: APPROVED]` string from a physical QA report to decide if a task is done.
5. **Punitive Loops**: If an agent breaks the contract (e.g., fails to write a required artifact), the system automatically intercepts the failure and subjects the agent to a reprimand prompt, forcing compliance.

By constraining the execution agents within this rigid framework, we paradoxically unlock their ability to handle much more complex, multi-step engineering tasks autonomously, reliably, and without the need for constant human supervision.