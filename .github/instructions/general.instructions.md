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

After completing a feature or non-trivial change, remind the user to run a multi-model code review:

```
/review using codex 5.3, opus 4.6, gemini 3 pro
```

After the review passes complete, offer to synthesize the findings into a consolidated report using the code-review-synthesis skill.
