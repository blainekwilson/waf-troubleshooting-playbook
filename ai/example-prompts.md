# Example AI Troubleshooting Prompts

Poor prompting often causes AI systems to reinforce unsupported assumptions.

This document provides examples of weak prompts and evidence-driven alternatives.

The goal is not to discourage AI use.

The goal is to improve troubleshooting quality by ensuring AI evaluates evidence rather than assumptions.

---

# Core Principle

> AI should help analyze evidence — not replace it.

Weak prompts often:

- assume ownership
- skip request-path validation
- encourage speculation
- treat technical possibility as proof

Stronger prompts:

- provide evidence
- identify known facts
- distinguish assumptions from findings
- request structured analysis

---

# Weak Prompt Example

## Bad Prompt

> “Could the WAF be causing this 403?”

Problems:

- assumes WAF involvement
- provides no evidence
- skips traversal validation
- encourages speculative answers

---

## Better Prompt

> “Users receive HTTP 403.
>
> Evidence currently available:
>
> - HAR file attached
> - raw HTTP response attached
> - no matching WAF logs found
> - origin infrastructure logs available
>
> Determine whether evidence confirms the request traversed the WAF before evaluating ownership.”

Benefits:

- requests evidence evaluation
- validates request path first
- avoids premature ownership assignment

---

# Weak Prompt Example

## Bad Prompt

> “The WAF is blocking our API calls. How do we fix it?”

Problems:

- assumes root cause
- lacks timestamps
- lacks evidence
- skips troubleshooting methodology

---

## Better Prompt

> “An API request returns HTTP 403.
>
> Evidence collected:
>
> - HAR file attached
> - raw HTTP response attached
> - timestamps available
> - no matching WAF logs for the request
> - application logs show direct-to-origin requests
>
> Determine which layer most likely generated the response and explain the supporting evidence.”

Benefits:

- provides evidence
- identifies known facts
- asks for ownership evaluation rather than confirmation bias

---

# WAF Traversal Validation Prompt

Before evaluating WAF ownership, validate whether the request traversed the WAF.

## Better Prompt

> “Users report an HTTP error.
>
> Evidence collected:
>
> - HAR file attached
> - raw HTTP response attached
> - timestamps available
>
> Determine whether evidence confirms the request traversed the WAF before evaluating root cause.”

Benefits:

- prioritizes traversal validation
- leverages direct request evidence
- avoids DNS-first assumptions

---

# Status Code Investigation Prompt

AI should distinguish between:

- possible
- likely
- proven
- disproven

This is particularly important for status code investigations.

## Weak Prompt

> “Can the WAF cause HTTP 426 errors?”

Problems:

- encourages possibility-based reasoning
- invites confirmation bias
- provides no evidence

A technically correct answer may still be operationally misleading.

---

## Better Prompt

> “We are seeing HTTP 426 responses.
>
> List the common non-WAF causes first.
>
> Then evaluate whether the WAF is involved using:
>
> - evidence supporting WAF involvement
> - evidence against WAF involvement
> - falsification tests
> - confidence level
> - next evidence to collect.”

Benefits:

- anchors troubleshooting in typical causes
- avoids WAF-first bias
- encourages structured uncertainty

---

# Second-Hand Information Prompt

AI should not treat summaries or opinions as authoritative evidence.

## Weak Prompt

> “The application team says the WAF is blocking traffic. What WAF rule should we change?”

Problems:

- accepts second-hand information
- assumes ownership
- bypasses evidence validation

---

## Better Prompt

> “The application team suspects the WAF is blocking traffic.
>
> Evidence currently available:
>
> - screenshots
> - timestamps
> - HAR file pending
> - no WAF event IDs collected
>
> Identify what evidence is needed before evaluating WAF ownership.”

Benefits:

- treats summaries as unverified
- requests missing evidence
- reinforces methodology

---

# AI-Assisted Evidence Collection

AI can be particularly useful when evidence is incomplete.

Rather than asking AI to determine root cause immediately, ask:

## Better Prompt

> “Here is the currently available troubleshooting evidence.
>
> Identify:
>
> - known facts
> - assumptions
> - missing evidence
> - competing explanations
> - next validation steps.”

Benefits:

- organizes investigations
- highlights evidence gaps
- prevents premature conclusions

---

# Recommended Troubleshooting Prompt Structure

Strong prompts typically include:

- timestamps
- affected URLs
- HAR files
- raw HTTP requests/responses
- WAF headers or fingerprints
- WAF event IDs
- source IP information
- proxy details
- application or origin logs
- reproduction steps
- known vs unknown information

The more clearly evidence is presented, the more reliable AI-assisted analysis becomes.

---

# Recommended Response Format

When evaluating WAF involvement or troubleshooting ownership, use the structured response format defined in:

→ [Troubleshooting Skill / Required Response Structure](troubleshooting-skill.md)

This format encourages:

- evidence-driven analysis
- explicit uncertainty
- falsification testing
- confidence scoring
- structured evaluation of ownership

---

# Related Content

- [Troubleshooting Skill](troubleshooting-skill.md)
- [Authoritative Sources](authoritative-sources.md)
- [Evidence Requirements](evidence-requirements.md)
- [Anti-Assumption Rules](anti-assumption-rules.md)