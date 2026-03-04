# Copilot Project Template

A language-agnostic GitHub Copilot framework template you can drop into any development project. Provides structured commit conventions, coding guidelines, and reusable Copilot skills for requirements refinement and reference lookups.

## Quick Start

Copy the Copilot configuration files into your project:

```bash
# Clone this template
git clone https://github.com/jkfrydendahl/copilot-project-template.git

# Copy into your project (adjust path)
cp copilot-project-template/.copilot-commit-message-instructions.md your-project/
cp -r copilot-project-template/.github your-project/
```

Or use this repo as a [GitHub template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) when creating new repositories.

## What's Included

```
.copilot-commit-message-instructions.md    # Commit message conventions
.github/
├── copilot-instructions.md                # 🔀 Top-level router — ties everything together
├── instructions/
│   ├── general.instructions.md            # Language-agnostic coding guidelines
│   └── code-review.instructions.md        # Review criteria & severity levels (auto-applied by /review)
└── skills/
    ├── code-review/                       # Multi-model review synthesis
    │   └── SKILL.md                       # Synthesis protocol (post-/review)
    ├── refine-requirements/               # Requirements → Architecture → Test Plan
    │   ├── SKILL.md                       # Skill definition & invocation
    │   ├── phases/
    │   │   ├── phase-1-discovery.md       # Understand requirements
    │   │   ├── phase-2-exploration.md     # Explore codebase, draft business rules
    │   │   ├── phase-3-architecture.md    # Design two approaches, user picks one
    │   │   └── phase-4-test-plan.md       # Write test plan, produce final output
    │   └── references/
    │       └── work-item-template.md      # Output template for work tracking tools
    └── reference-lookup/                  # External codebase & docs lookup
        ├── SKILL.md                       # Skill definition & procedure
        └── references/
            ├── sources.md                 # ⚙️ Configure your reference sources here
            └── search-patterns.md         # Tool-agnostic search heuristics
```

## Components

### Copilot Instructions Router

**File:** `.github/copilot-instructions.md`

Top-level configuration file that Copilot reads automatically. Routes to all coding guidelines, commit conventions, and available skills — ensuring Copilot picks up the full framework regardless of client.

### Commit Message Instructions

**File:** `.copilot-commit-message-instructions.md`

Structured conventional commit messages with:
- **Type + Scope** header (feat, fix, refactor, etc.)
- **Business Context** — why the change was made
- **Technical Changes** — what was modified
- **Implementation Details** — specific decisions and changes
- **Impact** — what's enabled, breaking changes, performance

### Coding Instructions

**File:** `.github/instructions/general.instructions.md`

Language-agnostic guidelines for Copilot:
- Build and test expectations
- Code quality standards
- Pointers to available skills

### Skill: `/refine-requirements`

A 4-phase workflow for analyzing work items before implementation:

| Phase | Focus | Output |
|-------|-------|--------|
| **1. Discovery** | Understand requirements, identify affected areas | Summary of scope and domains |
| **2. Exploration** | Explore codebase, draft and refine business rules | Business Rules Analysis table |
| **3. Architecture** | Design two approaches (Minimal vs Clean), user picks | Architecture document with diagrams |
| **4. Test Plan** | Write test scenarios using ZOMBIES methodology | Test plan with scenarios |

Each phase has a **user checkpoint** — Copilot won't proceed until you approve. The final output is a single Markdown block you can paste into your work tracking tool.

### Skill: `/review` (Multi-Model Code Review)

Two-part code review system:

1. **Review criteria** (`.github/instructions/code-review.instructions.md`) — automatically applied during every `/review` pass. Defines 7 review categories and 4 severity levels so each model evaluates against consistent standards.

2. **Synthesis skill** (`.github/skills/code-review/SKILL.md`) — run after `/review using codex 5.3, opus 4.6, gemini 3 pro` to consolidate the three independent passes into a deduplicated, confidence-scored, prioritized report.

### Skill: `/reference-lookup`

A configurable skill for exploring external codebases, documentation, and APIs:

1. **Configure sources** — edit `references/sources.md` with your project's reference repos, docs, and API specs
2. **Use the skill** — Copilot follows a structured procedure: identify sources → search → inspect → cross-check
3. **Get results** — file paths, function signatures, hook points, and recommended patterns

## Customization

### Add Language-Specific Instructions

Create additional instruction files in `.github/instructions/`:

```
.github/instructions/
├── general.instructions.md          # Included by default
├── typescript.instructions.md       # TypeScript-specific guidelines
├── python.instructions.md           # Python-specific guidelines
└── csharp.instructions.md           # C#-specific guidelines
```

### Configure Reference Sources

Edit `.github/skills/reference-lookup/references/sources.md` to add your project's reference sources:

```markdown
| Name | Type | Location | Description |
|------|------|----------|-------------|
| Django | repo | django/django | Django framework patterns |
| Project API | api-spec | docs/openapi.yaml | Our API contracts |
| Internal Wiki | docs | wiki.example.com | Team knowledge base |
```

### Add Project-Specific Skills

Create new skill folders in `.github/skills/` following the same pattern:

```
.github/skills/your-skill/
├── SKILL.md           # Skill definition with name, description, procedure
└── references/        # Supporting reference files
```

## License

[MIT](LICENSE)