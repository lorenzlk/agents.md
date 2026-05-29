# agents.md

A canonical, version-controlled **agent operating contract** for AI coding agents (Codex, Cursor, Claude Code, Windsurf). One authoritative file, with history preserved in git so it reads like the evolution of an operating manual.

## What Lives Here

- **`AGENTS.md`** — the primary artifact. A global operating contract covering:
  - **Compound engineering** — each unit of work makes the next easier; the Plan → Work → Review → Compound loop.
  - **Agent architecture** — the QMD (procedural memory) → Skills → Agent Loop → Tools/MCP flow.
  - **The agent harness** — the seven components around the LLM (context & memory, tools & action, orchestration, state, sandbox, observability, cost).
  - **Memory Bank protocol** — startup read order, initialization rules, and starter-file purposes for project continuity.
  - **Operating rules** — risk minimization, convention-following, dependency policy, communication standards, and git hygiene.
- `agents-mulanetworkreporting.md` — a project-specific extension (optional adoption path), kept for reference.
- Small supporting docs only when they clearly improve maintainability.

## How To Use It

Drop `AGENTS.md` at the root of a repo (or your global agent config). Repository-local `AGENTS.md` files override this global file within their scope. Keep active context small; store historical detail separately.

## Conventions

- `AGENTS.md` is the canonical file name for tool compatibility.
- Changes stay small, reviewable, and easy to verify.
- Commit messages explain *why* a change to the operating document matters.
- Do not commit from a sandboxed agent against this repo — stage or edit only, then commit from the host (see Git Hygiene in `AGENTS.md`).
