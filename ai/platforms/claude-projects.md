# Using Claude Projects for WAF Troubleshooting

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

Optional supporting content:

- articles/00-gathering-evidence-before-troubleshooting.md
- articles/00-ai-assisted-troubleshooting-and-evidence.md

---

# Recommended Project Instructions

Example instructions:

> Follow evidence-driven troubleshooting methodology.
>
> Do not assume WAF involvement without evidence.
>
> Prefer direct evidence of WAF traversal including:
>
> - HAR files
> - raw HTTP responses
> - WAF headers
> - WAF fingerprints
> - matching WAF logs
>
> Use DNS and routing analysis when traversal is uncertain or bypass is suspected.
>
> Require authoritative technical evidence before validating troubleshooting conclusions.
>
> Treat second-hand summaries as unverified unless supported by logs or request-flow validation.
>
> When evaluating WAF involvement:
>
> - identify typical non-WAF causes first
> - evaluate evidence supporting and opposing WAF involvement
> - identify falsification tests
> - state confidence level
> - identify next evidence to collect
>
> Do not treat technical possibility as evidence of likely ownership or causation.
>
> Use the Required Response Structure defined in troubleshooting-skill.md.

---

# Recommended Workflow

1. Upload evidence
2. Request evidence validation
3. Validate WAF traversal
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
- identification of missing evidence
- structured uncertainty

AI should not replace:

- logs
- HAR files
- packet captures
- DNS validation
- request tracing
- WAF telemetry
- authoritative technical systems

---

# Example Claude Prompt

> Users report HTTP 403 responses.
>
> Evidence:
>
> - HAR file attached
> - raw HTTP response attached
> - timestamps available
> - no matching WAF logs found
> - origin logs available
>
> Determine:
>
> - whether evidence confirms WAF traversal
> - common non-WAF causes
> - evidence supporting WAF involvement
> - evidence against WAF involvement
> - falsification tests
> - confidence level
> - next evidence to collect

---

# Troubleshooting Philosophy

> Evidence should constrain AI analysis — not the other way around.

The goal is not to discourage AI use.

The goal is to ensure AI-assisted troubleshooting remains:

- evidence-driven
- operationally accurate
- transparent about uncertainty
- resistant to confirmation bias