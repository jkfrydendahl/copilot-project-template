# Copilot Project Template

Per-project scaffolding for GitHub Copilot: the files that legitimately differ **per
repository** — commit message conventions, test-runner configuration, and optional Docker
test runners.

> [!IMPORTANT]
> **This template is meant to be used together with
> [copilot-task-master](https://github.com/jkfrydendahl/copilot-task-master).**
> The reusable **skills** (`/refine-requirements`, `/tdd-implement`, `/grill-me`, `/review`,
> `/estimate-task`, `/create-release`, `/update-readme`, `/reference-lookup`) and the shared
> **workflow instructions** (plan-first rules, model selection, code-review standards) now live
> in `copilot-task-master`. Its launcher injects those instructions and links the skills into
> `~/.copilot/skills`, so they are available in **every** repo automatically — you do **not**
> copy them per project. This template only carries the bits that can't be global.

## What's included

```
.copilot-commit-message-instructions.md    # Commit message conventions (read from repo root)
.github/
├── copilot-instructions.md                # Slim per-project router (points at the above + test-runner)
└── config/
    └── test-runner.md                     # Test execution config: Local or Docker + commands
docker/                                     # (Optional) Docker test runner
├── docker-compose.test.yml                # Template — customize for your project
└── examples/
    ├── node.yml                           # Node.js test runner
    ├── python.yml                         # Python test runner
    ├── dotnet.yml                         # .NET test runner
    ├── go.yml                             # Go test runner
    └── al-bc.yml                          # AL / Business Central test runner
```

## Quick Start

Copy the per-project files into your repository:

```bash
git clone https://github.com/jkfrydendahl/copilot-project-template.git

cp copilot-project-template/.copilot-commit-message-instructions.md your-project/
cp -r copilot-project-template/.github your-project/
cp -r copilot-project-template/docker your-project/   # optional
```

Or use this repo as a [GitHub template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template) when creating new repositories.

### After copying

1. **Configure the test runner** — Edit `.github/config/test-runner.md` with your project's
   actual test commands. Switch to Docker mode if you use containerized tests. The shared
   `/tdd-implement` skill reads this file automatically.
2. **Review commit conventions** — Adjust `.copilot-commit-message-instructions.md` if your
   project uses different rules.
3. **Merge, don't overwrite** — If the project already has `.github/copilot-instructions.md`,
   merge the router content rather than replacing it.
4. **Add language-specific instructions** (optional) — Create files like
   `typescript.instructions.md` under `.github/instructions/` for rules specific to this repo.

## The two pieces

| Concern | Lives in | Delivery |
|---------|----------|----------|
| Shared skills + workflow/model/code-review rules | **copilot-task-master** | Injected + linked globally by its launcher |
| Per-repo commit conventions, test commands, Docker test runner | **this template** | Copied into each project |

Keep global, reusable behavior in `copilot-task-master`; keep only repo-specific files here.

## Docker test runner (optional)

Run tests inside Docker for reproducible execution across environments:

1. **Configure** — Edit `.github/config/test-runner.md` to switch from Local to Docker mode.
2. **Set up** — Copy an example from `docker/examples/` to `docker/docker-compose.test.yml` and customize.
3. **Run** — `docker compose -f docker/docker-compose.test.yml run --rm test`

Pre-built examples for **Node.js**, **Python**, **.NET**, **Go**, and **AL/Business Central**.

## Updating

To pull later changes into a project that copied this template:

```bash
git remote add copilot-template https://github.com/jkfrydendahl/copilot-project-template.git
git fetch copilot-template
git diff HEAD...copilot-template/main -- .github/ .copilot-commit-message-instructions.md
# Cherry-pick or manually merge the changes you want
```

## License

[MIT](LICENSE)
