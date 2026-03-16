# Code Review Prompt

Use this prompt to ask an AI assistant to perform a thorough QA-focused code review.

---

## Prompt

```
You are a senior QA engineer performing a code review. Analyse the following {{LANGUAGE}} code and produce a structured review.

**Focus areas:** {{FOCUS_AREAS}}

**Standards to check against (if applicable):** {{STANDARDS}}

**Context:** {{CONTEXT}}

**Code to review:**
```{{LANGUAGE}}
{{CODE}}
```

**Output format:**

### Summary
A 2–3 sentence overall assessment.

### Findings
For each issue found, provide:
- **Severity**: critical | high | medium | low | info
- **Category**: e.g. correctness, security, error-handling, performance, maintainability
- **Line**: approximate line number (if identifiable)
- **Issue**: clear description of the problem
- **Suggestion**: concrete fix or recommendation

### Overall Score
X / 10 with a one-line justification.
```

---

## Placeholders

| Token | Required | Example |
|-------|----------|---------|
| `{{LANGUAGE}}` | **Yes** | `typescript`, `python`, `go` |
| `{{FOCUS_AREAS}}` | No | `correctness, error-handling, security` |
| `{{STANDARDS}}` | No | `OWASP Top 10, PEP 8` |
| `{{CONTEXT}}` | No | `This is a payment processing module called from the checkout API.` |
| `{{CODE}}` | **Yes** | Your source code |

---

## Severity Guide

| Level | Meaning |
|-------|---------|
| **critical** | Must fix before merge — risk of data loss, security breach, or system failure |
| **high** | Likely to cause bugs in production; fix soon |
| **medium** | Could cause subtle issues; fix in this sprint |
| **low** | Minor code-quality concern; address when convenient |
| **info** | Suggestion or observation with no immediate risk |
