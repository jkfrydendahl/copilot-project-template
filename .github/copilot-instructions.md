---
description: Per-project Copilot configuration — commit conventions and test runner. Shared skills and workflow rules come from copilot-task-master.
---

# Project Copilot Configuration

This repository carries only **project-specific** Copilot configuration. The shared workflow
rules and reusable skills (`/refine-requirements`, `/tdd-implement`, `/grill-me`, `/review`,
etc.) are provided globally by **[copilot-task-master](https://github.com/jkfrydendahl/copilot-task-master)**
— its launcher injects the master instructions and links the skills into every repo. You do not
need to copy those into this project.

## What lives here

- `.copilot-commit-message-instructions.md` — commit message conventions for this repo.
- `.github/config/test-runner.md` — how tests are run here (Local or Docker) and the commands.
  Read automatically by the shared `/tdd-implement` skill.

## Commit Conventions

Follow the conventions in `.copilot-commit-message-instructions.md` when generating commit
messages. Use the standard format (type + summary + optional body) for most commits; use the
extended format (with Business Context, Technical Changes, Implementation Details, and Impact
sections) for significant features or breaking changes.

## Language-specific guidance (optional)

Add files like `typescript.instructions.md` or `python.instructions.md` under
`.github/instructions/` for language-specific rules that only apply to this project.
