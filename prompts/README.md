# Prompts

Reusable, parameterised prompt templates for common QA tasks. Each template is written in Markdown and uses `{{PLACEHOLDER}}` tokens for variable content. Copy a template, replace the placeholders, and paste it into your AI assistant of choice.

## Available Prompts

| File | Purpose |
|------|---------|
| [`generate-tests.md`](generate-tests.md) | Ask an AI to write tests for existing code |
| [`code-review.md`](code-review.md) | Ask an AI to perform a QA-focused code review |
| [`bug-analysis.md`](bug-analysis.md) | Ask an AI to diagnose a bug and suggest a fix |
| [`test-plan.md`](test-plan.md) | Ask an AI to produce a structured test plan |
| [`coverage-analysis.md`](coverage-analysis.md) | Ask an AI to identify coverage gaps |

## Usage

1. Open the relevant `.md` file.
2. Replace all `{{PLACEHOLDER}}` tokens with real content.
3. Paste the resulting prompt into your AI assistant (Copilot Chat, Claude, ChatGPT, etc.).

Alternatively, use the JSON tool definitions in [`../tools/`](../tools/) to let the AI call these capabilities automatically via function calling.

## Placeholder Convention

| Token | Meaning |
|-------|---------|
| `{{LANGUAGE}}` | Programming language (e.g. `python`, `typescript`) |
| `{{CODE}}` | Source code snippet |
| `{{FRAMEWORK}}` | Testing framework (e.g. `pytest`, `jest`) |
| `{{FEATURE}}` | Feature or user-story name |
| `{{REQUIREMENTS}}` | Requirements or acceptance criteria |
