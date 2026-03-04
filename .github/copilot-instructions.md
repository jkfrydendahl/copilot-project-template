---
description: Top-level Copilot instructions — routes to coding guidelines, skills, and conventions.
---

# Project Copilot Configuration

This project uses a structured Copilot framework with coding instructions, commit conventions, and reusable skills.

## Coding Instructions

Follow the guidelines in `.github/instructions/`:
- `general.instructions.md` — Language-agnostic coding standards (always active)
- Add language-specific files (e.g., `typescript.instructions.md`) as needed

## Commit Conventions

Follow the conventions in `.copilot-commit-message-instructions.md` when generating commit messages. Use conventional commit format with Business Context, Technical Changes, Implementation Details, and Impact sections.

## Available Skills

### `/refine-requirements`
4-phase planning workflow: Discovery → Exploration → Architecture → Test Plan.
Use before implementing any non-trivial feature or change.
See `.github/skills/refine-requirements/SKILL.md`.

### `/reference-lookup`
Look up patterns, APIs, and implementations in external codebases and documentation.
Configure project-specific sources in `.github/skills/reference-lookup/references/sources.md`.
See `.github/skills/reference-lookup/SKILL.md`.

### `/review` (Multi-Model Code Review)
Run three independent review passes using diverse AI models, then synthesize into a prioritized report.
Invoke with: `/review using codex 5.3, opus 4.6, gemini 3 pro`
See `.github/skills/code-review/SKILL.md`.
