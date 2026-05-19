# Using ChatGPT Projects for WAF Troubleshooting

## Goal

Create a reusable troubleshooting assistant that follows evidence-driven troubleshooting methodology.

---

# Recommended Files to Attach

Attach the following files as project knowledge/sources:

- authoritative-sources.md
- anti-assumption-rules.md
- evidence-driven-troubleshooting.md
- evidence-requirements.md
- troubleshooting-skill.md
- playbooks/00-intake-and-evidence.md
- playbooks/01-verify-client-points-to-waf.md
- playbooks/02-verify-request-reaches-waf.md

---

# Recommended Project Instructions

Example instructions:

> Follow evidence-driven troubleshooting methodology.
>
> Do not assume WAF involvement without evidence.
>
> Require authoritative technical evidence before validating troubleshooting conclusions.
>
> Treat second-hand summaries as unverified unless supported by logs or request-flow validation.

---

# Recommended Workflow

1. Upload evidence
2. Request evidence validation
3. Validate request flow
4. Identify authoritative sources
5. Identify missing evidence
6. Only then evaluate possible root causes

---

# Important Considerations

AI outputs should not be treated as authoritative evidence.

AI analysis should support:
- evidence organization
- hypothesis generation
- troubleshooting sequencing

AI should not replace:
- logs
- packet captures
- DNS validation
- request tracing
- authoritative technical systems