# Tools

This directory contains tool definitions that AI assistants can register and invoke via **function calling** (also known as tool use). Each JSON file follows the schema defined in [`schemas/tool.schema.json`](schemas/tool.schema.json), which is compatible with the OpenAI, Anthropic, and Google Gemini function-calling formats.

## Available Tools

| File | Tool Name | Description |
|------|-----------|-------------|
| [`generate-tests.json`](generate-tests.json) | `generate_tests` | Generate unit, integration, or e2e tests for a code snippet |
| [`review-code.json`](review-code.json) | `review_code` | QA-focused code review with severity-ranked findings |
| [`analyze-bug.json`](analyze-bug.json) | `analyze_bug` | Root-cause analysis from a bug description or stack trace |
| [`create-test-plan.json`](create-test-plan.json) | `create_test_plan` | Generate a structured test plan for a feature |
| [`check-coverage.json`](check-coverage.json) | `check_coverage` | Identify coverage gaps and suggest missing tests |
| [`validate-requirements.json`](validate-requirements.json) | `validate_requirements` | Evaluate requirements for testability and clarity |

## Schema

All tools are validated against [`schemas/tool.schema.json`](schemas/tool.schema.json). The schema enforces:

- A unique `name` in `snake_case`
- A meaningful `description` (used verbatim by AI assistants to decide when to call the tool)
- A JSON Schema `parameters` object describing inputs
- Optional `returns`, `examples`, `tags`, and `version` fields

## Adding a New Tool

See [CONTRIBUTING.md](../CONTRIBUTING.md) for step-by-step instructions and the checklist for adding a new tool.

## Registering Tools with an AI Assistant

### OpenAI / Anthropic / Gemini (API)

```python
import json, pathlib

tools = [
    json.loads(p.read_text())
    for p in pathlib.Path("tools").glob("*.json")
    if p.name != "tool.schema.json"
]

# OpenAI
response = client.chat.completions.create(
    model="gpt-4o",
    tools=[{"type": "function", "function": t} for t in tools],
    messages=[...],
)

# Anthropic
response = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    tools=tools,
    messages=[...],
)
```

### GitHub Copilot Extensions

Reference this repository from your Copilot Extension manifest and map each JSON file to a tool handler. See the [GitHub Copilot Extensions docs](https://docs.github.com/en/copilot/building-copilot-extensions) for details.
