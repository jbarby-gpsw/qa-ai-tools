# Generate Tests Prompt

Use this prompt to ask an AI assistant to generate tests for an existing piece of code.

---

## Prompt

```
You are an expert QA engineer. Generate comprehensive {{TEST_TYPE}} tests for the following {{LANGUAGE}} code using {{FRAMEWORK}}.

**Requirements:**
- Cover the happy path, edge cases, and error conditions.
- Use descriptive test names that explain the scenario (e.g. `test_returns_empty_list_when_input_is_none`).
- Mock any external dependencies (database, HTTP calls, file I/O).
- Add a brief inline comment for each test explaining *what* it verifies and *why*.
- Aim for at least 80% branch coverage.

**Additional scenarios to cover:**
{{COVERAGE_TARGETS}}

**Source code:**
```{{LANGUAGE}}
{{CODE}}
```

Return only the complete, runnable test file. Include all necessary imports.
```

---

## Placeholders

| Token | Required | Example |
|-------|----------|---------|
| `{{TEST_TYPE}}` | No (default: `unit`) | `unit`, `integration`, `e2e` |
| `{{LANGUAGE}}` | **Yes** | `python`, `typescript`, `go` |
| `{{FRAMEWORK}}` | No (inferred) | `pytest`, `jest`, `go test` |
| `{{COVERAGE_TARGETS}}` | No | `- null/empty inputs\n- concurrent access` |
| `{{CODE}}` | **Yes** | Your source code |

---

## Example (filled in)

```
You are an expert QA engineer. Generate comprehensive unit tests for the following Python code using pytest.

Requirements:
- Cover the happy path, edge cases, and error conditions.
- Use descriptive test names that explain the scenario.
- Mock any external dependencies.
- Add a brief inline comment for each test.
- Aim for at least 80% branch coverage.

Additional scenarios to cover:
- Negative numbers
- Zero division
- Very large floats

Source code:
```python
def divide(a: float, b: float) -> float:
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b
```
```
