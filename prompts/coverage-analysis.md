# Coverage Analysis Prompt

Use this prompt to ask an AI assistant to identify gaps in your existing test suite and suggest new tests to fill them.

---

## Prompt

```
You are a QA engineer specialising in test coverage. Analyse the following source code and existing tests to identify coverage gaps.

**Language:** {{LANGUAGE}}

**Minimum coverage target:** {{MINIMUM_COVERAGE}}%

**Source code:**
```{{LANGUAGE}}
{{SOURCE_CODE}}
```

**Existing tests:**
```{{LANGUAGE}}
{{EXISTING_TESTS}}
```

**Coverage report (optional):**
```
{{COVERAGE_REPORT}}
```

**Output format:**

### Estimated Current Coverage
X% (based on branch/line analysis)

### Does It Meet the Target?
Yes / No — brief explanation.

### Coverage Gaps
For each gap:
- **Type**: branch | line | error-path | edge-case
- **Priority**: high | medium | low
- **Description**: what code path is not tested
- **Suggested Test**: name and one-line description of a test to add

### Summary
2–3 sentences summarising the overall coverage situation and recommended next steps.
```

---

## Placeholders

| Token | Required | Example |
|-------|----------|---------|
| `{{LANGUAGE}}` | **Yes** | `python`, `typescript`, `java` |
| `{{MINIMUM_COVERAGE}}` | No (default: 80) | `90` |
| `{{SOURCE_CODE}}` | **Yes** | Source file or function to analyse |
| `{{EXISTING_TESTS}}` | No | Existing test file or list of test names |
| `{{COVERAGE_REPORT}}` | No | Output from pytest-cov, Istanbul, JaCoCo, etc. |
