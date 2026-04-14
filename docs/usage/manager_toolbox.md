# The Manager Toolbox

The Manager (Layer 2) has access to a set of flat scripts in the `tools/` directory to interact with Cortex. These tools abstract away the complexity of artifact generation and orchestration.

## Available Commands

### 1. `init_project.py`
Scaffolds a standard `GEMINI.md` file in a target project directory. This file acts as the project's "Brain" (Project Knowledge).

```bash
python tools/init_project.py /path/to/my-project
```

### 2. `implement_feature.py` (The Dispatch Engine)
This is the primary tool for dispatching work to Layer 1. Calling this tool is the **reward for a successful clarification phase**. 

Once the Manager and the human reach the "Certainty Threshold" regarding a feature, the Manager calls this tool with a detailed summary. 

```bash
python tools/implement_feature.py /path/to/my-project --summary "Add a logout button that clears local storage..."
```

**What happens under the hood:**
1.  **The Desk Work (Headless Manager)**: The tool spawns a transient, headless instance of the Manager. This instance acts as a bureaucratic clerk, compiling the `summary` into the rigid, Space-Grade Engineering Specifications (`IRQ.md` and `QAR.md`) and writing them to the disk.
2.  **The Loop**: Once the artifacts are generated, the tool automatically hands execution over to `implementation_run.py`, triggering the headless Doer <-> QA state machine on the Factory Floor.

#### The `--git-gate` Flag
When dispatching a feature, you can enable "Git Gating". This forces the orchestrator to verify that the Git workspace is clean (no uncommitted changes) before starting the run on a new branch.

```bash
python tools/implement_feature.py /path/to/my-project --summary "..." --git-gate
```

---

## Strategic Interaction (The Manager's Workflow)

As the Layer 2 Architect, you should follow this sequence for every request:

1.  **The Boardroom (Interrogation)**: Clarify the user's intent. Ask sharp, relevant questions until the "Certainty Threshold" is reached.
2.  **The Desk Work (Dispatch)**: Run `implement_feature.py` to silently generate the contracts and dispatch the Layer 1 workers.
3.  **Audit**: Review the final `QRP.md` and report back to the human.
4.  **Grow**: If the human is unhappy, update the project's `GEMINI.md` with a new ritual and repeat.