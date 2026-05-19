# AI-Assisted Troubleshooting Starts With Evidence

AI tools have quickly become part of operational troubleshooting.

Engineers now routinely ask AI systems questions such as:

- “Could the WAF be causing this error?”
- “Why am I getting a 403?”
- “Could this be a firewall issue?”
- “What layer usually causes this response?”

AI can be extremely useful during troubleshooting.

It can:

- summarize information
- organize findings
- explain technologies
- compare possible causes
- suggest additional troubleshooting steps

However, AI can also unintentionally reinforce unsupported assumptions when prompts contain incomplete, inaccurate, or second-hand information.

This creates a new operational problem:

> AI responses are sometimes treated as evidence.

They should not be.

---

# A Common Failure Pattern

A common troubleshooting pattern looks like this:

1. An error occurs
2. A system is suspected
3. AI is asked whether that system could cause the issue
4. AI confirms the possibility
5. The AI response becomes supporting evidence
6. Troubleshooting narrows prematurely

For WAF teams, this often sounds like:

> “Could the WAF be causing this 403?”

An AI system may respond:

> “Yes, WAFs commonly cause 403 responses due to blocking rules or policy configuration.”

While technically possible, this response does not prove:

- the request traversed the WAF
- the WAF generated the response
- the WAF evaluated the request
- the WAF caused the failure

The answer may be plausible.

Plausibility is not proof.

---

# AI Is Most Useful After Evidence Is Collected

The problem is not AI.

The problem is incomplete troubleshooting inputs.

AI performs best when constrained by evidence.

Before asking AI to evaluate possible root causes, gather technical evidence.

Examples include:

- timestamps
- screenshots
- HAR files
- raw HTTP requests and responses
- WAF event IDs
- source IP information
- proxy details
- application logs
- reproduction steps

This aligns directly with:

→ [Step 00: Intake and Evidence Review](../playbooks/00-intake-and-evidence.md)

---

# Evidence First, AI Second

One of the most common troubleshooting mistakes is skipping request-path validation.

Before evaluating WAF policy behavior, determine whether evidence confirms the request traversed the WAF.

Strong evidence may include:

- HAR files
- raw HTTP responses
- WAF response headers
- WAF fingerprints
- matching WAF logs

Supporting evidence may include:

- DNS validation
- internal vs external resolution
- routing configuration
- hardcoded IP validation

AI can help interpret these findings.

AI should not replace them.

---

# AI Should Help Collect Missing Evidence

Poor AI interaction often looks like:

## Weak Prompt

> “Could the WAF be causing this?”

This prompt:

- assumes WAF involvement
- provides no evidence
- encourages speculation
- bypasses troubleshooting methodology

A stronger interaction looks like:

## Better Prompt

> “Internal users receive HTTP 403 while external users succeed.
>
> HAR file attached.
>
> No matching WAF logs found for the request timestamp.
>
> Internal DNS resolves the hostname differently than external DNS.
>
> Determine whether evidence suggests the request traversed the WAF.”

This approach:

- provides context
- includes evidence
- identifies authoritative sources
- encourages analysis rather than speculation

---

# AI Instructions and Troubleshooting Skills

To improve consistency, this project includes reusable AI troubleshooting guidance.

These files are intended for:

- ChatGPT projects
- Claude projects
- internal AI assistants
- troubleshooting copilots
- reusable prompt libraries

The guidance focuses on:

- evidence-driven troubleshooting
- authoritative sources
- reducing assumption amplification
- request-path validation
- structured troubleshooting methodology

The goal is simple:

> AI should assist troubleshooting methodology — not replace it.

---

# Evidence Is Still the Authority

AI can accelerate troubleshooting.

It can help identify gaps and organize investigations.

But AI should not become the authority.

The authoritative sources remain:

- logs
- packet captures
- HAR files
- DNS validation
- WAF telemetry
- application evidence
- request tracing

Evidence should constrain AI analysis.

Not the other way around.

---

# Related Content

- [Step 00: Intake and Evidence Review](../playbooks/00-intake-and-evidence.md)
- [AI Guidance](../ai/README.md)
- [Authoritative Sources](../ai/authoritative-sources.md)
- [Anti-Assumption Rules](../ai/anti-assumption-rules.md)
- [Example Prompts](../ai/example-prompts.md)