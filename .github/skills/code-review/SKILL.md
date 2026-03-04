---
name: code-review
description: "Multi-model code review protocol. Runs three independent review passes using diverse AI models, then synthesizes findings into a consolidated, prioritized report."
---

# Multi-Model Code Review

Structured code review protocol that leverages three diverse AI models for independent, full-scope reviews. Each model reviews the complete changeset independently, then findings are synthesized into a single prioritized report.

## Why Multi-Model?

Different models have different strengths, blind spots, and reasoning styles. Running three independent passes dramatically increases coverage:
- Findings confirmed by multiple models are high-confidence
- Findings from only one model may reveal blind spots the others missed
- Disagreements between models highlight areas that need human judgment

## Invocation

```
/review using codex 5.3, opus 4.6, gemini 3 pro
```

This triggers three independent review passes across the changeset.

## Review Models

| Model | ID | Strengths |
|-------|----|-----------|
| **GPT-5.3-Codex** | `gpt-5.3-codex` | Strong at logic flow, algorithmic correctness, and spotting subtle bugs |
| **Claude Opus 4.6** | `claude-opus-4.6` | Strong at architectural reasoning, design patterns, and security implications |
| **Gemini 3 Pro** | `gemini-3-pro-preview` | Strong at edge cases, type safety, and cross-cutting concerns |

> **Note**: Model strengths are generalizations. The key value is in *diversity of perspective*, not any single model's specialization.

## Review Scope

Each model independently reviews the **full changeset** against all criteria below. No focus-area partitioning — every model covers everything.

## Review Criteria

Each review pass must evaluate the changeset against these categories:

### 1. Correctness & Logic
- Does the code do what it claims to do?
- Are there logic errors, off-by-one errors, or incorrect conditions?
- Are return values and error states handled correctly?
- Are edge cases covered (null, empty, zero, boundary values)?

### 2. Security
- Are there injection vulnerabilities (SQL, XSS, command injection)?
- Is user input validated and sanitized?
- Are secrets/credentials handled safely (no hardcoding, proper env vars)?
- Are authorization checks present where needed?
- Are there race conditions or TOCTOU vulnerabilities?

### 3. Performance
- Are there unnecessary allocations, loops, or database calls?
- Are N+1 query patterns present?
- Is caching used appropriately (or missing where needed)?
- Are there blocking operations that should be async?

### 4. Error Handling
- Are errors caught and handled gracefully?
- Are error messages informative without leaking internals?
- Are transactions/rollbacks handled correctly?
- Is there proper cleanup in failure paths (resources, connections)?

### 5. Design & Architecture
- Does the change follow existing project patterns?
- Is the responsibility clearly assigned (no god objects/functions)?
- Are abstractions appropriate (not over- or under-engineered)?
- Are dependencies reasonable and well-directed?

### 6. Maintainability
- Is the code readable and self-documenting?
- Are names clear and consistent with the project's conventions?
- Are there magic numbers or unclear constants?
- Is test coverage adequate for the change?

### 7. Breaking Changes & Compatibility
- Does this break existing APIs, contracts, or behavior?
- Are migrations or data changes backward-compatible?
- Are deprecations properly signaled?

## Severity Levels

Each finding must be classified:

| Severity | Meaning | Action |
|----------|---------|--------|
| 🔴 **Critical** | Bug, security vulnerability, data loss risk | Must fix before merge |
| 🟠 **Warning** | Performance issue, design concern, missing validation | Should fix before merge |
| 🟡 **Suggestion** | Improvement, readability, minor optimization | Consider for this or future PR |
| ℹ️ **Note** | Observation, question, or discussion point | No action required |

## Synthesis Protocol

After all three models complete their independent reviews:

### 1. Deduplicate
Group findings that describe the same issue. Note which models flagged it.

### 2. Confidence Score
Rate each unique finding by how many models independently identified it:

| Models | Confidence | Interpretation |
|--------|------------|----------------|
| 3/3 | **High** | Very likely a real issue |
| 2/3 | **Medium** | Probably worth addressing |
| 1/3 | **Low** | May be a false positive, or a genuine blind-spot catch — review carefully |

### 3. Prioritize
Sort findings by: Severity (descending) → Confidence (descending) → Category.

### 4. Output Format

Present the synthesized report:

```markdown
## Code Review Summary

**Changeset**: [PR/branch description]
**Models Used**: GPT-5.3-Codex, Claude Opus 4.6, Gemini 3 Pro

### Findings

| # | Severity | Category | Finding | Confidence | Models | File(s) |
|---|----------|----------|---------|------------|--------|---------|
| 1 | 🔴 Critical | Security | [Description] | High (3/3) | All | `src/auth.ts:42` |
| 2 | 🟠 Warning | Performance | [Description] | Medium (2/3) | Codex, Gemini | `src/db.ts:88` |
| 3 | 🟡 Suggestion | Design | [Description] | Low (1/3) | Opus | `src/service.ts:15` |

### Details

#### Finding 1: [Title]
- **Severity**: 🔴 Critical
- **Category**: Security
- **Confidence**: High (3/3 models)
- **Location**: `src/auth.ts:42`
- **Description**: [What's wrong]
- **Recommendation**: [How to fix]

### Summary
- **Critical**: N findings (must fix)
- **Warning**: N findings (should fix)
- **Suggestion**: N findings (consider)
- **Notes**: N observations
```

## Tips

1. **Don't skip synthesis** — Raw output from three models is noisy. The synthesis step is where the value is.
2. **Pay attention to lone findings** — A single model catching something the others missed is often the most valuable finding.
3. **Use for non-trivial changes** — Simple typo fixes don't need three-model review. Use this for features, refactors, and security-sensitive changes.
4. **Iterate if needed** — After addressing critical/warning findings, you can re-run the review to verify fixes.
