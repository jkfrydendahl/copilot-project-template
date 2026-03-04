---
description: General development guidelines — building, testing, and available tools
---

# Build & Test

Always build and test the project before returning results to the user. The build must complete with zero errors. If errors are reported, resolve them and rebuild until clean before responding.

Use the project's existing build and test commands (e.g., `make`, `npm run build`, `dotnet build`, `cargo build`, `go build`, etc.). Do not introduce new build tools unless the project has none.

# Code Quality

- Follow existing code conventions and patterns found in the repository.
- Match the project's naming conventions, file organization, and architectural patterns.
- Write minimal, focused changes — do not refactor unrelated code.
- Add or update tests when changing behavior.
- Update documentation when changing public APIs or user-facing behavior.

# Available Skills

- Use `/refine-requirements` to analyze and plan work items before implementation.
- Use `/reference-lookup` to find patterns, APIs, or implementations in external codebases and documentation.

# Post-Implementation Review

After completing a feature or non-trivial change, **perform a self-review** of your own changes before returning to the user:

1. Analyze the diff of all changes made during this task
2. Evaluate against the review criteria in `.github/instructions/code-review.instructions.md`
3. Classify any findings by severity (🔴 Critical, 🟠 Warning, 🟡 Suggestion, ℹ️ Note)
4. If Critical or Warning findings are found, fix them before presenting the work to the user
5. Present a brief review summary alongside the completed work

After the self-review, suggest the user run a multi-model review for deeper coverage:

> For additional coverage with multiple AI models, run:
> ```
> /review using codex 5.3, opus 4.6, gemini 3 pro
> ```
> Then ask Copilot to synthesize the findings using the code-review-synthesis skill.
