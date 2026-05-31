# agents.md

A canonical, version-controlled **agent operating contract** for AI coding agents (Codex, Cursor, Claude Code, Windsurf). One authoritative file, with history preserved in git so it reads like the evolution of an operating manual.

## What Lives Here

- **`AGENTS.md`** — the primary artifact. A global operating contract covering:
  - **Compound engineering** — each unit of work makes the next easier; the Plan → Work → Review → Compound loop.
  - **Agent architecture** — the QMD (procedural memory) → Skills → Agent Loop → Tools/MCP flow.
  - **The agent harness** — the seven components around the LLM (context & memory, tools & action, orchestration, state, sandbox, observability, cost).
  - **Memory Bank protocol** — startup read order, initialization rules, and starter-file purposes for project continuity.
  - **Operating rules** — risk minimization, convention-following, dependency policy, communication standards, and git hygiene.
- `templates/CLAUDE.md` — reusable stub that redirects Cowork / Claude Code to `AGENTS.md`; copy into a new project root.
- `CHANGELOG.md` — versioned history so adopters can pin a contract version.
- `agents-mulanetworkreporting.md` — a project-specific extension (optional adoption path), kept for reference.
- Small supporting docs only when they clearly improve maintainability.

## How To Use It

This repo is the canonical source of the contract. New projects are their own git repos that pull `AGENTS.md` down at setup.

One-command bootstrap (after installing `init-agents` on your `PATH`):

```bash
init-agents my-new-project          # latest contract from main
init-agents my-app --version v1.0.0 # pin a tagged version
```

It fetches `AGENTS.md` + `CLAUDE.md`, scaffolds `memory-bank/` (with a `projectbrief.md` skeleton), and makes the initial commit. Install once:

```bash
ln -s "$(pwd)/init-agents" /usr/local/bin/init-agents
```

Repository-local `AGENTS.md` files override the global contract within their scope. Keep active context small; store historical detail separately.

## Conventions

- `AGENTS.md` is the canonical file name for tool compatibility.
- Changes stay small, reviewable, and easy to verify.
- Commit messages explain *why* a change to the operating document matters.
- Do not commit from a sandboxed agent against this repo — stage or edit only, then commit from the host (see Git Hygiene in `AGENTS.md`).
