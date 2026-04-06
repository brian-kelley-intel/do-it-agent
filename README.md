# do-it-agent

Multi-agent orchestrator plugin for Copilot CLI. Takes a prompt through intent
analysis, implementation planning, wave-based coding, and quality grading —
fully automated from idea to PR.

## How It Works

```
User Prompt
    │
    ▼
┌─────────────────────────────────┐
│       do-it-orchestrator        │
│                                 │
│  Phase 1 → Analyzer             │  Understand intent, explore codebase
│  Phase 2 → Planner              │  Create implementation plan + docs
│  Phase 3 → Plan Reviewer        │  Validate plan (loop if needed)
│  Phase 4a → QA Contract         │  Agree on quality criteria
│  Phase 4b → Implementor         │  Wave-based implementation
│  Phase 5 → Grader               │  Grade against QA contract
│           ↺ (loop 4b–5)         │  Fix issues and re-grade
│  Phase 6 → Finalize             │  Push branch, create PR, check CI
└─────────────────────────────────┘
```

### Agents

| Agent | Role |
|-------|------|
| **do-it-orchestrator** | Pipeline coordinator — manages state and dispatches phases |
| **do-it-analyzer** | Explores codebase, parses intent, identifies risks |
| **do-it-planner** | Creates implementation plan with feature waves and decision records |
| **do-it-plan-reviewer** | Validates plan for completeness, simplicity, and feasibility |
| **do-it-implementor** | Negotiates QA criteria and implements code wave-by-wave |
| **do-it-grader** | Sets quality standards and grades implementation with structured verdicts |

### File Handoff

All inter-agent state is managed through the filesystem:

```
.do-it/runs/<run-id>/
├── state.json              # Pipeline state (phase, iteration, verdicts)
├── analysis/
│   └── context.md          # Intent, codebase map, risks
├── plan/
│   ├── plan.md             # Master implementation plan
│   ├── feature_split.md    # Wave breakdown and order
│   ├── decisions.md        # Architecture decision records
│   ├── gotchas.md          # Edge cases and pitfalls
│   ├── evidence.md         # Code references
│   └── quality_plan.md     # Agreed QA contract
├── reviews/
│   └── plan_review_N.md    # Plan reviewer findings
└── iterations/
    └── N/
        └── grade_report.md # Structured grader verdict
```

## Quick Start — Copilot Plugin

This repository ships as a **Copilot CLI / VS Code plugin**
([docs](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-creating)).

| File | Purpose |
|------|---------|
| `plugin.json` | Plugin manifest |
| `skills/do-it/SKILL.md` | Skill trigger and documentation |
| `agents/*.agent.md` | Agent definitions |

### 1. Install the plugin

**Copilot CLI:**

```bash
copilot plugin install brian-kelley-intel/do-it-agent
```

**VS Code:**

1. Open **Preferences → Open User Settings (JSON)** and add the marketplace:

   ```jsonc
   "chat.plugins.marketplaces": [
       "brian-kelley-intel/do-it-agent"
   ],
   ```

2. In the Copilot chat panel, type `/plugins` and install **do-it-agent**.

### 2. Use it

Ask Copilot to implement something:

- *"Implement a REST API for user authentication with JWT tokens"*
- *"Add a dark mode toggle to the settings page"*
- *"Refactor the database layer to use connection pooling"*
- *"Do it — build the feature described in issue #42"*

The orchestrator will analyze, plan, implement, and grade — then open a PR.

### 3. Monitor progress

Check the run state at any time:

```bash
cat .do-it/runs/*/state.json
```

Review plan artifacts in `.do-it/runs/<run-id>/plan/`.

## Design Principles

1. **Simplest complete solution** — every decision favors simplicity over cleverness
2. **Wave-based implementation** — features are built and tested incrementally
3. **Quality-gated** — grader must pass before PR is created
4. **Transparent state** — all inter-agent communication is visible in `.do-it/`
5. **Fail-safe** — errors are surfaced, never swallowed; max iteration caps prevent loops

## Development

```bash
# Clone and install locally
git clone https://github.com/brian-kelley-intel/do-it-agent.git
cd do-it-agent
copilot plugin install .

# Verify installation
copilot plugin list
```

## License

MIT
