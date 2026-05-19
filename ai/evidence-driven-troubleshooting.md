# Evidence-Driven Troubleshooting

Troubleshooting should be driven by technical evidence, not assumptions or system reputation.

This is especially important when using AI systems during investigations.

---

# Common Failure Pattern

A common troubleshooting failure pattern:

1. An error occurs
2. The WAF is suspected
3. AI is asked whether the WAF could cause the issue
4. AI confirms the possibility
5. The AI response is treated as evidence
6. Investigation focuses on the WAF before validating request flow

This often results in:

- delayed root cause identification
- incorrect escalations
- wasted troubleshooting effort
- incomplete investigations

---

# Recommended Workflow

## Step 00 — Review Existing Evidence

Collect:

- timestamps
- screenshots
- HAR files
- request/response samples
- logs
- DNS results

---

## Step 01 — Verify Request Path

Confirm:
- DNS resolution
- proxy path
- WAF traversal
- origin connectivity

---

## Step 02 — Validate Layer-by-Layer

Validate each system independently:

- DNS
- WAF
- load balancer
- web server
- application

---

## Step 03 — Use AI to Assist Analysis

Once evidence is collected:

- summarize findings
- identify gaps
- suggest additional validation steps
- compare competing hypotheses

---

# Core Principle

> Evidence should constrain AI analysis — not the other way around.

---

# Related Content

- [Step 00: Intake and Evidence Review](../playbooks/00-intake-and-evidence.md)
- [Anti-Assumption Rules](anti-assumption-rules.md)