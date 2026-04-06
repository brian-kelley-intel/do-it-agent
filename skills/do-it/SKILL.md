---
name: do-it
description: >-
  Orchestrates multi-agent implementation pipeline: analyzes intent, creates
  implementation plans, implements in waves, and grades quality — from prompt
  to PR. Use when asked to implement a feature, build something, create a PR,
  or when the user says "do it", "build this", "implement", or "make it happen".
---

# Do-It: Multi-Agent Implementation Pipeline

Automates the full cycle from user prompt to merged PR using six coordinated
agents. Invoke the orchestrator to start.

## Quick Start

When the user describes a feature or task to implement, invoke the orchestrator:

```
Use the do-it-orchestrator agent to implement: <user's request>
```

The orchestrator runs six phases automatically:

1. **Analyze** — understand intent, explore codebase, identify constraints
2. **Plan** — create implementation plan with supporting docs
3. **Review** — validate plan for completeness and simplicity
4. **QA Contract** — implementor and grader agree on quality criteria
5. **Implement + Grade** — wave-based implementation with quality checks
6. **Finalize** — create branch, PR, verify CI

## Agents

| Agent | Phase | Purpose |
|-------|-------|---------|
| `do-it-orchestrator` | All | Top-level pipeline coordinator |
| `do-it-analyzer` | 1 | Intent analysis and codebase exploration |
| `do-it-planner` | 2 | Implementation plan generation |
| `do-it-plan-reviewer` | 3 | Plan validation and critique |
| `do-it-implementor` | 4a, 4b | QA negotiation and wave-based coding |
| `do-it-grader` | 4a, 5 | QA contract and structured quality grading |

## File Handoff

All state lives in `.do-it/runs/<run-id>/`. See the orchestrator agent for
the full directory layout and state management protocol.

## When to Use

- User asks to implement a feature end-to-end
- User wants automated planning before implementation
- User wants quality-gated implementation with CI verification
- User says "do it", "build this", "implement this", "make it happen"

## When NOT to Use

- Quick one-file edits (just do them directly)
- Exploratory questions about code (use grep/view)
- Tasks that don't produce code changes
