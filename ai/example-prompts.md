# Example AI Troubleshooting Prompts

Poor prompting often causes AI systems to reinforce unsupported assumptions.

This document provides examples of weak prompts and evidence-driven alternatives.

---

# Weak Prompt Example

## Bad Prompt

> “Could the WAF be causing this 403?”

Problems:

- assumes WAF involvement
- provides no evidence
- skips request flow validation
- encourages speculative answers

---

# Improved Prompt Example

## Better Prompt

> “The application returns a 403 for internal users only.
>
> External users succeed.
>
> Internal DNS resolves the hostname to an internal IP.
>
> No matching WAF logs exist for the failed requests.
>
> Determine whether evidence suggests the WAF handled the request.”

Benefits:

- provides evidence
- identifies request scope
- references authoritative sources
- avoids assumption-driven troubleshooting

---

# Weak Prompt Example

## Bad Prompt

> “The WAF is blocking our API calls. How do we fix it?”

Problems:

- assumes root cause
- lacks timestamps
- lacks evidence
- lacks request flow validation

---

# Improved Prompt Example

## Better Prompt

> “An API request returns HTTP 403.
>
> Evidence collected:
>
> - HAR file attached
> - DNS resolution attached
> - No WAF logs for the request timestamp
> - Application logs show direct-to-origin requests from internal systems
>
> Determine which layer most likely generated the response.”

---

# Recommended Troubleshooting Prompt Structure

Provide:

- timestamps
- source IPs
- DNS resolution
- HAR files
- request/response samples
- WAF event IDs
- proxy details
- request path information
- application log evidence

---

# Related Content

- [Authoritative Sources](authoritative-sources.md)
- [Anti-Assumption Rules](anti-assumption-rules.md)