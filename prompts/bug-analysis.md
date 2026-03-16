# Bug Analysis Prompt

Use this prompt to ask an AI assistant to diagnose a bug, identify the root cause, and propose a fix.

---

## Prompt

```
You are an expert software debugger. Analyse the following bug report and produce a structured root-cause analysis.

**Bug description:**
{{DESCRIPTION}}

**Stack trace / error message:**
```
{{STACK_TRACE}}
```

**Relevant source code ({{LANGUAGE}}):**
```{{LANGUAGE}}
{{CODE_SNIPPET}}
```

**Steps to reproduce:**
{{STEPS_TO_REPRODUCE}}

**Environment:**
{{ENVIRONMENT}}

**Output format:**

### Root Cause
A clear, concise statement of the most likely root cause.

### Hypotheses (ranked by confidence)
1. [High/Medium/Low confidence] — Hypothesis description and supporting evidence
2. ...

### Fix Suggestions
For each hypothesis, provide a concrete code change or remediation step, including a code patch where appropriate.

### Regression Tests to Add
List 2–5 test case names (and brief descriptions) that would prevent this bug from recurring.
```

---

## Placeholders

| Token | Required | Example |
|-------|----------|---------|
| `{{DESCRIPTION}}` | **Yes** | `Service crashes when user has no email set.` |
| `{{STACK_TRACE}}` | No | Paste the full stack trace |
| `{{LANGUAGE}}` | No | `python`, `java`, `typescript` |
| `{{CODE_SNIPPET}}` | No | Relevant source code |
| `{{STEPS_TO_REPRODUCE}}` | No | Numbered list of reproduction steps |
| `{{ENVIRONMENT}}` | No | `Python 3.12, Django 5.0, PostgreSQL 16` |
