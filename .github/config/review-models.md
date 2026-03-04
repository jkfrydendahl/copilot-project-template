# Review Models Configuration

Configure the AI models used for multi-model code review. Update this file when newer or better models become available — all review references point here.

## Models

| Model | Review Command Name | Model ID | Strengths |
|-------|-------------------|----------|-----------|
| **GPT-5.3-Codex** | `codex 5.3` | `gpt-5.3-codex` | Code-focused reasoning, implementation detail |
| **Claude Opus 4.6** | `opus 4.6` | `claude-opus-4.6` | Broad analysis, architectural thinking |
| **Gemini 3 Pro** | `gemini 3 pro` | `gemini-3-pro-preview` | Alternative perspective, pattern recognition |

## Review Command

```
/review using codex 5.3, opus 4.6, gemini 3 pro
```

Update the model names in the table above **and** the review command when changing models. The "Review Command Name" column shows the exact string used in the `/review using ...` command.
