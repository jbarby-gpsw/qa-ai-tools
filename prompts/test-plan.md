# Test Plan Prompt

Use this prompt to ask an AI assistant to generate a comprehensive, structured test plan for a feature or user story.

---

## Prompt

```
You are a senior QA engineer. Create a comprehensive test plan for the following feature.

**Feature:** {{FEATURE}}

**Requirements / Acceptance Criteria:**
{{REQUIREMENTS}}

**Test types to include:** {{TEST_TYPES}}

**Known risk areas:** {{RISK_AREAS}}

**Out of scope:** {{OUT_OF_SCOPE}}

**Target environment:** {{ENVIRONMENT}}

**Output format:**

### Objective
One paragraph describing what this test plan aims to verify.

### Scope
**In scope:** (bullet list)
**Out of scope:** (bullet list)

### Entry Criteria
Conditions that must be true before testing can start.

### Exit Criteria
Conditions that must be met to consider testing complete.

### Test Cases
For each test case:
| ID | Title | Type | Priority | Preconditions | Steps | Expected Result |
|----|-------|------|----------|---------------|-------|-----------------|

Priority: critical | high | medium | low

### Risks and Mitigations
Known risks and how to address them.
```

---

## Placeholders

| Token | Required | Example |
|-------|----------|---------|
| `{{FEATURE}}` | **Yes** | `User Login` |
| `{{REQUIREMENTS}}` | **Yes** | Acceptance criteria or user story text |
| `{{TEST_TYPES}}` | No | `unit, integration, security, performance` |
| `{{RISK_AREAS}}` | No | `account lockout, SQL injection` |
| `{{OUT_OF_SCOPE}}` | No | `OAuth login, password reset` |
| `{{ENVIRONMENT}}` | No | `staging` |

---

## Tips

- Be as specific as possible in `{{REQUIREMENTS}}`. Vague requirements produce vague test plans.
- List concrete risk areas to ensure they receive dedicated test cases.
- Attach any relevant wireframes or API specs in the prompt for richer output.
