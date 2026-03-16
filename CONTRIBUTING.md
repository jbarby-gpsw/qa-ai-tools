# Contributing to qa-ai-tools

Thank you for contributing! This document explains how to add new tools and prompt templates so the repository stays consistent and usable by any AI assistant.

## Table of Contents

- [Adding a New Tool](#adding-a-new-tool)
- [Adding a New Prompt Template](#adding-a-new-prompt-template)
- [Validating Your Changes](#validating-your-changes)
- [Commit Message Convention](#commit-message-convention)
- [Code of Conduct](#code-of-conduct)

---

## Adding a New Tool

Tools are JSON files in the `tools/` directory that follow the schema defined in `tools/schemas/tool.schema.json`. They use the OpenAI/Anthropic function-calling format so any modern AI assistant can register and invoke them.

### Checklist

- [ ] Create `tools/<your-tool-name>.json` (use kebab-case for the filename)
- [ ] Set `name` to a `snake_case` identifier (this becomes the function name the AI calls)
- [ ] Write a clear `description` — this is the *only* signal the AI uses to decide when to call the tool
- [ ] Define all input parameters in `parameters.properties` with types and descriptions
- [ ] List required parameters in `parameters.required`
- [ ] Add at least one realistic `examples` entry showing a complete input/output pair
- [ ] Add relevant `tags` (e.g. `"testing"`, `"review"`, `"coverage"`)
- [ ] Set `version` to `"1.0.0"` for new tools
- [ ] Validate the JSON against the schema (see [Validating Your Changes](#validating-your-changes))
- [ ] Add a row to the table in `tools/README.md`
- [ ] Add a row to the table in the root `README.md`
- [ ] Add a corresponding prompt template in `prompts/` (see below)
- [ ] Add a row to the prompts table in `prompts/README.md`

### Tool Naming

| Good | Avoid |
|------|-------|
| `analyze_accessibility` | `check` (too vague) |
| `generate_api_contract` | `myTool` (camelCase) |
| `validate_openapi_spec` | `tool1` (meaningless) |

### Description Tips

The `description` field is what the AI reads to decide *whether* to call your tool. Make it:
- **Action-oriented**: start with a verb ("Generate", "Analyse", "Validate")
- **Specific**: say what the tool does and when it is useful
- **Concise**: one to three sentences

---

## Adding a New Prompt Template

Prompts in `prompts/` are Markdown files containing a ready-to-use prompt with `{{PLACEHOLDER}}` tokens.

### Checklist

- [ ] Create `prompts/<your-prompt-name>.md`
- [ ] Include a short description at the top explaining when to use the prompt
- [ ] Wrap the prompt text in a fenced code block so it is easy to copy
- [ ] Document every `{{PLACEHOLDER}}` in a table with: token name, whether it is required, and an example value
- [ ] Provide a filled-in example at the bottom of the file
- [ ] Add a row to the table in `prompts/README.md`

---

## Validating Your Changes

The CI workflow at `.github/workflows/validate.yml` automatically validates all JSON files in `tools/` against `tools/schemas/tool.schema.json` using [ajv-cli](https://github.com/ajv-validator/ajv-cli).

To run the validation locally:

```bash
npm install -g ajv-cli@5
ajv validate -s tools/schemas/tool.schema.json -d "tools/*.json" --strict=false
```

---

## Commit Message Convention

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(tools): add validate_openapi_spec tool
fix(tools): correct required fields in generate_tests
docs(prompts): add accessibility-review prompt template
chore: update README tool table
```

---

## Code of Conduct

Be respectful and constructive. All contributions are welcome, from fixing typos to adding entirely new tool categories.
