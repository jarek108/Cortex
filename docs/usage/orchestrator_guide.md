# Orchestrator Guide (E2E Workflows)

The orchestrator (`implementation_run.py`) is the engine that drives Layer 1 (The Factory Floor) of the Cortex OS. It manages the agent loop, enforces the artifact contract, and manages the Git-Native State Machine.

> **Note:** As a human user, you rarely need to invoke `implementation_run.py` directly. You interact with Layer 2 (The Manager), which automatically dispatches the orchestrator via the `implement_feature.py` tool.

## Basic Usage

If you have manually drafted an `IRQ.md` (Implementation Request) and `QAR.md` (QA Request) in your workspace and want to trigger the factory floor directly:

```bash
python implementation_run.py --workspace /path/to/my-project
```

## Configuration (`run_config.json`)

The orchestrator's behavior is dictated by a JSON configuration. When dispatched by Layer 2, this is generated automatically in the Central Registry, but you can provide overrides via the CLI.

### Configuration Parameters

*   **`doer_model` / `qa_model`**: The Gemini models to use for the respective roles (e.g., `gemini-3-flash-preview`).
*   **`max_iters`**: The maximum number of Doer->QA loops before the orchestrator forcefully aborts the run (default: 3).
*   **`registry_base`**: Override the default location of the Central Registry (where telemetry is stored).
*   **`memory_and_context`**:
    *   `doer_amnesia_frequency`: How often the Doer's internal session ID is reset. `1` means a fresh session every iteration.
    *   `qa_amnesia_frequency`: How often the QA's internal session ID is reset.

## Advanced Overrides via CLI

You can override key parameters directly from the command line:

```bash
python implementation_run.py \
  --workspace ./my-project \
  --doer-model gemini-1.5-pro \
  --max-iters 10
```

## Observability and Monitoring

Because Cortex uses Git as the State Machine, the terminal output of `implementation_run.py` is intentionally quiet, showing only high-level phase transitions and Git commit notifications.

To deep-dive into what the agents are doing:

1. **The Glass**: Run `python tools/dashboard.py` and open `http://localhost:8080`. This provides a live, visual representation of the Git state machine and the LLM's internal monologue.
2. **Git Log**: Because the orchestrator executes on a dedicated feature branch (`gemini-run-<id>`), you can simply run `git log` or `git diff` in your workspace to view the exact changes made at each "Time Travel Checkpoint."
3. **The Registry**: Navigate to `~/.gemini/orchestrator/runs/run_<id>/` to view the `run_state.json` (which contains exact USD cost calculations) and the `logs/` directory for raw API responses.