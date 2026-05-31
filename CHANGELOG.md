# Changelog

All notable changes to the agent operating contract are recorded here. Adopters can pin a tagged version.

The format is loosely based on [Keep a Changelog](https://keepachangelog.com/). Versioning is semantic at the contract level: MAJOR for breaking changes to required behavior, MINOR for new sections or capabilities, PATCH for clarifications and fixes.

## [1.0.0] - 2026-05-30

First versioned release of the expanded global contract.

### Added
- Global multi-tool operating contract (Codex / Cursor / Claude Code / Windsurf): core principles, Memory Bank protocol, dependency policy, communication standards, repository overrides.
- Compound engineering philosophy and the Plan → Work → Review → Compound loop.
- Agent architecture flow: QMD (procedural memory) → Skills → Agent Loop → Tools/MCP.
- The seven-component agent harness (context & memory, tools & action, orchestration, state, sandbox, observability, cost).
- Git Hygiene section (no sandbox commits; clear stale locks).
- `templates/CLAUDE.md` reusable stub that redirects Cowork/Claude Code to `AGENTS.md`.
- `init-agents` bootstrap script: fetches the contract (latest or pinned), scaffolds `memory-bank/` with a seeded `projectbrief.md`, and makes the initial commit.
- README refreshed to reflect the contract's scope and one-command setup.

### Notes
- `agents-mulanetworkreporting.md` remains a project-specific extension (optional adoption path), unchanged.
