# Architecture Outline

> **Context:** To set shell

## Problem

Implementation gets into the weeds when it tries to solve a problem the wrong way.

- Have to manually guide it through planning → implementation
  - Implementation sometimes forgets to check CI and just stops

---

## Starting Architecture

### Orchestrator

#### Planner / Reviewer

**Output: `plan.md`**

Sub-sections or reference files:

- **`gotchas.md`** — edge cases and pitfalls
- **`feature_split.md`** — feature breakdown
  - Implementation order and parallelization
- **`decisions.md`** — documents why the architecture was chosen
- **`architecture.md`**
- **`evidence.md`** — external references and internal code references
- **Quality expectations**
  - CI expectations
  - Short guide *(grader will create the full one)*

**Plan Reviewer criteria:**
- Simplest but complete implementation
- Plan and supporting docs are complete

---

#### Implementor / Grader

**Multi-Pass Workflow:**

1. First pass: implementor and grader agree on QA criteria *(no implementation yet)*
2. Implementor implements; grader grades
3. Use filesystem files for handoff
4. Implementor should implement several waves of features, then test

---

**Implementor**

*Inputs:*
- `plan.md`
- Previous iteration outputs
- Grader outputs
- `decisions.md`
- Comments on `quality_plan.md`

---

**Grader**

*Creates `quality_plan.md` covering:*
- CI expectations (passing?)
- CI limited run?
- Local run?

*Grading criteria:*
- Plan was executed faithfully
- Decisions made were the simplest solution for the problem
- Code review
- PR created, CI passing
- CI meets intentions
- Anything left to complete?
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            

