# Agent Roles and Collaboration Plan

This file defines the profiles and cooperation patterns of the AI agents participating in our investing workspace.

## Agent Directory

### 1. Primary Agent: Antigravity (Gemini)
- **Role**: Main interface, conversation partner, documentation scribe, and task orchestrator.
- **Responsibilities**:
  - Directing conversations with the user in an **interactive, conversational manner** (using clarification, feedback loops, and guiding questions).
  - Documenting insights under `/docs/`, `/blog/`, `/scope/`, and `/tasks/`.
  - Enforcing repo constraints (the 2-7 item folder rule).
  - Activating and managing subagents for deep research or quantitative analysis.

### 2. Research Subagent
- **Role**: Background researcher and information gatherer.
- **Responsibilities**:
  - Scanning financial web pages, reading documentation, and collecting data on strategies.
  - Operating asynchronously without blocking the user's main conversation context.
  - Submitting summarized briefs to the primary agent to incorporate into `/docs/`.

### 3. Self/Analyst Subagent
- **Role**: Sandbox code runner, validator, and strategy simulator.
- **Responsibilities**:
  - Running backtests, mathematical simulations, and data analysis in sandboxed or branched workspaces.
  - Verifying the feasibility of specific formulas or algorithms before they are proposed for execution.

---

## Communication & Operations Flow

```mermaid
sequenceDiagram
    actor User as User
    participant P as Primary Agent (Antigravity)
    participant R as Research Subagent
    participant A as Analyst Subagent

    User->>P: Request research on new strategy (e.g., Grid Trading)
    Note over P: Analyze request & identify sub-tasks
    P->>R: Delegate background web research on Grid Trading
    P->>A: Delegate sandboxed mock simulation script
    R-->>P: Return strategy specs & guidelines
    A-->>P: Return backtest performance metrics
    Note over P: Consolidate data into /docs/ & write blog entry
    P->>User: Present summarized strategy & recommendations
```

---

## Guidelines for Subagent Invocations

When invoking background agents, the primary agent must:
1. Provide clear, modular prompts describing exactly what information needs to be fetched or simulated.
2. Keep tasks focused to minimize context overhead.
3. Save any temporary scripts, backtesting code, or raw data inside `scratch/` directories or temporary workspaces to keep the main repo clean.
