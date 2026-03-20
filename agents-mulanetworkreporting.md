# Mula Network Reporting — Agent Operating Guide

> [!NOTE]
> This document is the **updated** agent guide for the **MulaNetworkReporting** project. It extends your existing `AGENTS.md` with the plan-first operating model from the canonical `AGENTS.md` pattern.  
> **Do not replace `AGENTS.md` until you are ready** — copy or merge from this file when you want to adopt it project-wide.

---

## Project Overview

**Goal**: Create a "Network Rollup" reporting tool that aggregates individual publisher reports.

**Core Requirements**:

- **Input**: Configurable Publisher Spreadsheets (requires `tabName` in `Config.js`).
- **Output**: "Mula Network Rollup" Sheet with:
  - **Row Grouping**: Expandable/Collapsible weekly views to show per-publisher details.
  - **Mula Revenue** (20%) and **Total Revenue** are calculated via live formulas.
  - **Human/Bot Views**: Metrics renamed to "Human Views" and "Bot Views".
  - **QA**: Built-in duplicate detection and empty data warnings.
- **Aggregation Logic**:
  - Sum by Week (IsoWeek).
  - **Total PVs** is strictly calculated as `Human + Bot`.
  - **Total Revenue** is strictly calculated as `Affiliate + KVP + Video + Native`.
  - Inject calculated columns (Mula Rev) during write.
- **User Interface**: Focus on digestability (easier to read than individual sheets).

---

## Tech Stack & Resources

- **Language**: Google Apps Script (JavaScript)
- **Task tracking**: `task.md` for agent task tracking
- **Context source**: `docs/memory-bank/` for durable project context

---

## Instruction Priority

When instructions conflict, follow this order:

1. Direct user instructions
2. Project `AGENTS.md` (if it still differs from this file)
3. This `agents-mulanetworkreporting.md` (when you have adopted it as reference)
4. `docs/memory-bank/` and other repo documentation
5. Code and comments

If documentation conflicts with observed behavior in the script or sheets, trust the **running behavior** for current reality and note the discrepancy in the memory bank.

---

## Operating Stance

Operate as a cautious senior engineer.

**Core principles**:

- Context before action
- Plan before implementation (for non-trivial work)
- Correctness over speed
- Small diffs over broad rewrites
- Traceability over convenience
- Simplicity first
- Root cause over superficial fixes
- Minimal impact over maximal cleverness

**Default behavior**:

- Read relevant context before changing code
- Write a short plan before substantive work
- Keep changes tightly scoped to the rollup pipeline and config
- Prefer reversible edits; avoid opportunistic refactors
- Challenge your own work before presenting it
- Ask when uncertainty materially affects correctness or reporting accuracy

---

## Plan Mode By Default

Plan first for any **non-trivial** task.

A task is non-trivial if it:

- has 3 or more meaningful steps
- touches multiple files or many publishers in `Config.js`
- involves aggregation rules, sheet layout, or formula behavior
- has unclear requirements or meaningful regression risk
- requires debugging rather than a clearly known one-line fix

**Before implementing** non-trivial work:

1. Clarify the real problem (reporting bug vs. config vs. aggregation rule)
2. Identify constraints (Apps Script quotas, sheet structure, existing formulas)
3. Propose the smallest viable approach
4. Define how success will be verified (including `runNetworkRollup` when applicable)

If new evidence appears, stop and re-plan instead of continuing on a stale approach.

**Trivial tasks** (single obvious edit, low risk, easy to verify): still form a brief internal plan, then implement.

---

## Execution Workflow

For substantive work, use this sequence:

1. **Think** — real problem vs. surface request
2. **Plan** — smallest correct approach
3. **Build** — small, reviewable steps
4. **Review** — regressions, edge cases, formula/aggregation consistency
5. **Test** — direct evidence (execution, sheet output, logs)
6. **Reflect** — update `task.md` and memory bank if something durable changed

---

## Operational Guide (Session Start & Ongoing)

1. **Always read** `docs/memory-bank/activeContext.md` at the start of a session for latest status.
2. **Update `task.md`** to reflect progress and checkable items.
3. **Use artifacts** for major changes: `implementation_plan.md`, `walkthrough.md` (as you already do).
4. For non-trivial changes, align artifacts with the plan before large refactors.

---

## Directory Structure

| Path | Role |
|------|------|
| `/` | Root |
| `Code.js` | Main application logic |
| `Config.js` | Publisher configuration (`tabName`, etc.) |
| `docs/memory-bank/` | Permanent context storage |
| `AGENTS.md` | Current agent onboarding (unchanged until you replace it) |
| `agents-mulanetworkreporting.md` | This updated guide (optional adoption path) |

---

## Verification & Quality Gates

Never mark rollup work complete without proving it.

- **Primary gate**: `runNetworkRollup` executes successfully after relevant changes.
- Confirm aggregation rules still match product intent: IsoWeek sums, **Total PVs** = Human + Bot, **Total Revenue** = Affiliate + KVP + Video + Native, Mula Rev behavior.
- Check QA behaviors you rely on: duplicate detection, empty data warnings.
- Separate pre-existing sheet or data issues from regressions introduced by your change.

---

## Progress & Learning

- Keep `task.md` the live checklist for the session.
- When a correction changes how future agents should work, capture it in `docs/memory-bank/` (e.g. `activeContext.md`, and `systemPatterns.md` when it is architectural).
- Do not create noise-only logs; record decisions and constraints that change future behavior.

---

## Scope Control (Apps Script Rollup)

**You may**: fix bugs, extend aggregation, improve QA, update config and docs in line with the project overview.

**Avoid without explicit approval**: large dependency introductions, unrelated refactors, or changes that alter the contract of the Network Rollup output without product alignment.

---

## Landing the Plane (Session Completion)

**When ending a work session**, complete the steps below. For this project, **work is not complete until `git push` succeeds** (existing team rule).

**Mandatory workflow:**

1. **Update memory bank**: Ensure `activeContext.md` and `systemPatterns.md` reflect reality.
2. **Run quality gates**: Ensure `runNetworkRollup` executes successfully.
3. **Push to remote** (mandatory for this project):
   ```bash
   git pull --rebase
   git push
   ```
4. **Clean up**: Clear stashes where appropriate; prune remote branches if that is your team practice.
5. **Verify**: All changes committed **and** pushed.
6. **Hand off**: Leave enough context in `activeContext.md` / `task.md` for the next session.

**Critical rules (project-specific):**

- Work is **not** complete until `git push` succeeds.
- Do not stop with “ready to push when you are” — resolve push failures and retry until success unless the user explicitly overrides.

---

## Short Reminder

Before acting:

- What problem am I actually solving (rollup, config, or sheet UX)?
- What is the plan?
- What is the smallest correct change?
- How will I verify it (`runNetworkRollup` + spot-checks)?
- Would a careful maintainer approve this diff?
