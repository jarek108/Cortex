# The Amnesia Engine & Accumulative Knowledge

Have you ever argued with an AI, and it just keeps apologizing but repeating the exact same broken code? 

This is a well-known AI problem called **Anchoring Bias**. When an AI writes a flawed piece of code in Iteration 1, and you (or the QA agent) point out the flaw, the AI often spends Iterations 2, 3, and 4 stubbornly trying to patch its bad idea rather than taking a step back and rewriting it correctly. The longer the chat history gets, the more "anchored" the AI becomes to its original mistake. Furthermore, a massive context window slows down generation and increases API costs dramatically.

To solve this, Cortex implements the **Amnesia Engine** on the Factory Floor (Layer 1).

By forcing the execution agents to "go to sleep" and wake up with no memory of their past mistakes, we force them to look at the problem with fresh eyes.

## Hard Resets via Configuration

The system enforces session amnesia by wiping the agent's conversation history. This is controlled via the `run_config.json` generated during dispatch:

```json
"memory_and_context": {
  "doer_amnesia_frequency": 1,
  "qa_amnesia_frequency": 1
}
```

When frequency is set to `1`, the agent gets a completely fresh session ID on *every single iteration*. It wakes up with zero memory of the conversation that happened in previous rounds.

## Rebuilding Context: Accumulative Knowledge

If the agent has amnesia, how does it know what to fix? How does it avoid making the exact same mistake again?

Instead of relying on the messy, unstructured "train of thought" stored in standard LLM chat histories, or concatenating massive backlogs of old files, Cortex uses **Accumulative Knowledge**.

1. **The QA Summarizes the Past**: In every iteration, the QA agent reads the *current* code and its own *previous* QA Report (`QRP.md`). 
2. **The Trajectory Section**: The QA is explicitly prompted to summarize the history of the entire run into the "Trajectory & Loop Detection" section of the *new* `QRP.md`. (e.g., *"In Iteration 1 we tried X. In Iteration 2 we tried Y. Neither worked because of Z."*)
3. **The XML Injection**: Before waking the amnesic Doer agent for Iteration 3, the Orchestrator reads this single, highly compressed `QRP.md` directly from the Git feature branch and injects it physically into the system prompt:

```xml
<historical_feedback type="QRP" mode="accumulative">
---
id: QRP-v2
outcome: to correct
...
# Trajectory & Loop Detection
The Doer is oscillating between breaking the mobile view and the desktop view...
...
</historical_feedback>
```

### Why this is vastly superior:
1. **Curated Signal**: The agent only sees the *final, approved feedback* from the QA, not the messy trial-and-error thoughts it had while writing the bad code.
2. **Cognitive Reset**: By waking up fresh but with a clear, accumulative "bug report" (the XML payload), the LLM approaches the problem from first principles again, breaking the anchoring bias.
3. **Context Efficiency**: Instead of passing 50,000 tokens of chat history back and forth, or passing 5 separate `v1_QRP.md` files from a hidden registry, we pass a single, highly compressed, 500-token Markdown artifact that evolves dynamically on the Git branch.