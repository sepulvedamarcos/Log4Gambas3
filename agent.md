# Agent Guide for Gambas3 Projects

## Purpose

This file captures the minimum context an agent should read before modifying this repository.

## Project identity

- Project: `Log4Gambas3`
- Type: Gambas3 library project with a demo form
- Main reusable source: `.src/Clase/Log4Gambas3.class`
- Demo UI: `.src/FMain.class`, `.src/FMain.form`

## Mandatory Gambas3 assumptions

1. Gambas is **case-insensitive**.
2. `.class` files are **plain text source files**.
3. `.form` files are **plain text source files**.
4. `.gambas` files are **generated/binary artifacts**.
5. `.gambas/`, `.desc/`, `.info`, `.startup`, `.settings`, generated images and backups are not equivalent to hand-authored source code.

## Safe editing rules

- Prefer editing `.src/Clase/Log4Gambas3.class` for reusable behavior.
- Avoid changing `.src/FMain.form` unless the task is specifically UI-related.
- Prefer extracting or documenting logic over mixing more responsibility into forms.
- Do not rely on case-only renames.
- Be cautious with Gambas IDE generated files; they may create noisy diffs.

## Naming conventions to enforce

- Use explicit names; avoid near-collisions under case-insensitive resolution.
- Boolean names should prefer `Is`, `Has`, or `Should`.
- Keep terminology consistent between UI/demo code and reusable library code.
- Distinguish clearly between:
  - source files
  - generated artifacts
  - packaging metadata

## Repository map

- `README.md` — English technical readme
- `readme-es.md` — Spanish technical readme
- `.src/Clase/Log4Gambas3.class` — logging library
- `.src/FMain.class` — demo controller
- `.src/FMain.form` — demo UI
- `.project` — Gambas project definition
- `.component` — component metadata
- `spec.md` — architecture findings
- `tasks.md` — backlog

## Known technical findings

- Message formatting likely loses the timestamp due to assignment/concatenation logic.
- Log filename generation currently leaves a trailing space.
- Max file size is configured but not enforced.
- Rotation scans `*.log` in the directory, not only the current app prefix.

## Skills recommended for future sessions

- `gambas3-modern-dev`
- `project-documentation`
- `clean-code`
- `solid-architect-advisor` when architecture expands

## MCP / memory guidance

- Use Engram at session start/end.
- Save decisions about:
  - Gambas naming conventions
  - generated-vs-source file policy
  - documentation structure
  - safe refactor boundaries
- In this environment there are no project-specific MCP resources/templates registered yet.

## First checks for every new session

1. Read `agent.md`
2. Read `spec.md`
3. Read `tasks.md`
4. Check `git status`
5. Confirm whether IDE-generated changes are intentional before editing source
