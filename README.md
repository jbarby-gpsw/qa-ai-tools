# qa-ai-tools

A curated collection of QA tools and prompt templates that any AI coding assistant — GitHub Copilot, Claude, ChatGPT, Cursor, Aider, and others — can register and use to accelerate quality-assurance tasks.

---

## What Is This?

`qa-ai-tools` gives AI assistants a shared, version-controlled set of:

| Artefact | Location | Purpose |
|----------|----------|---------|
| **Tool definitions** | `tools/*.json` | JSON function schemas (OpenAI/Anthropic format) for AI function calling |
| **Prompt templates** | `prompts/*.md` | Reusable, parameterised prompts for common QA tasks |
| **AI configurations** | `.github/copilot-instructions.md`, `CLAUDE.md`, `.cursorrules` | Per-assistant behaviour rules that load automatically |
| **Integration bundles** | `integrations/` | Pre-built tool arrays ready to paste into API calls |

---

## Available Tools

| Tool | JSON file | When an AI should use it |
|------|-----------|--------------------------|
| `generate_tests` | [`tools/generate-tests.json`](tools/generate-tests.json) | Write unit, integration, or e2e tests for existing code |
| `review_code` | [`tools/review-code.json`](tools/review-code.json) | QA-focused code review with severity-ranked findings |
| `analyze_bug` | [`tools/analyze-bug.json`](tools/analyze-bug.json) | Root-cause analysis from a bug description or stack trace |
| `create_test_plan` | [`tools/create-test-plan.json`](tools/create-test-plan.json) | Produce a structured test plan for a feature |
| `check_coverage` | [`tools/check-coverage.json`](tools/check-coverage.json) | Identify coverage gaps and suggest missing tests |
| `validate_requirements` | [`tools/validate-requirements.json`](tools/validate-requirements.json) | Evaluate requirements for testability and clarity |

---

## Quick Start

### Option A — Paste a Prompt (no setup)

Copy any template from [`prompts/`](prompts/), fill in the `{{PLACEHOLDER}}` tokens, and paste it into your AI assistant.

### Option B — Register Tools via API (function calling)

```python
import json
from openai import OpenAI  # or anthropic, google.generativeai, etc.

client = OpenAI()

# Load the pre-built bundle
tools = json.load(open("integrations/openai/openai-tools.json"))

response = client.chat.completions.create(
    model="gpt-4o",
    tools=tools,
    messages=[{"role": "user", "content": "Write pytest tests for this function: ..."}],
)
```

See [`integrations/openai/README.md`](integrations/openai/README.md) for a full example.

### Option C — Point Your AI Assistant at This Repo

| Assistant | How to load these rules |
|-----------|------------------------|
| **GitHub Copilot** | `.github/copilot-instructions.md` is loaded automatically in any workspace |
| **Claude** | `CLAUDE.md` is loaded automatically when Claude Code is run in this directory |
| **Cursor** | `.cursorrules` is loaded automatically in any Cursor workspace |
| **Aider** | Run `aider --read CLAUDE.md` or add `read: CLAUDE.md` to `.aider.conf.yml` |
| **ChatGPT / API** | Register the tools in `integrations/openai/openai-tools.json` as custom functions |

---

## Repository Structure

```
qa-ai-tools/
├── tools/                        # Tool definitions (JSON, function-calling format)
│   ├── schemas/
│   │   └── tool.schema.json      # Master JSON Schema for validating tool files
│   ├── generate-tests.json
│   ├── review-code.json
│   ├── analyze-bug.json
│   ├── create-test-plan.json
│   ├── check-coverage.json
│   └── validate-requirements.json
│
├── prompts/                      # Reusable Markdown prompt templates
│   ├── generate-tests.md
│   ├── code-review.md
│   ├── bug-analysis.md
│   ├── test-plan.md
│   └── coverage-analysis.md
│
├── integrations/
│   └── openai/
│       ├── openai-tools.json     # Pre-built bundle for OpenAI / Anthropic APIs
│       └── README.md
│
├── .github/
│   ├── copilot-instructions.md   # GitHub Copilot custom instructions
│   └── workflows/
│       └── validate.yml          # CI: validates all tool JSON against schema
│
├── CLAUDE.md                     # Claude AI instructions (loaded automatically)
├── .cursorrules                  # Cursor IDE rules (loaded automatically)
├── CONTRIBUTING.md               # How to add new tools and prompts
└── README.md                     # This file
```

---

## Adding a New Tool

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full checklist. The short version:

1. Create `tools/<name>.json` following `tools/schemas/tool.schema.json`.
2. Add a prompt template in `prompts/<name>.md`.
3. Update the tables in `tools/README.md` and this `README.md`.
4. Regenerate `integrations/openai/openai-tools.json` (instructions in `integrations/openai/README.md`).
5. The CI workflow will validate the JSON automatically.

---

## Validation

All JSON files in `tools/` are validated against `tools/schemas/tool.schema.json` on every push via GitHub Actions ([`.github/workflows/validate.yml`](.github/workflows/validate.yml)).

To run validation locally:

```bash
npm install -g ajv-cli@5
ajv validate -s tools/schemas/tool.schema.json -d "tools/*.json" --strict=false
```

---

## Contributing

Contributions of new tools, prompt templates, and integrations are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

---

## License

MIT
