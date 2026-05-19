# Gathering Evidence Before Troubleshooting

When web applications fail, teams often want immediate answers.

Questions usually sound like:

- “Is the WAF blocking this?”
- “Could the firewall be causing it?”
- “Is the load balancer down?”
- “The application team says it isn’t the app — now what?”

The pressure to restore service quickly is understandable.

Unfortunately, troubleshooting often begins before sufficient evidence has been collected.

This creates a predictable problem:

> Troubleshooting becomes driven by assumptions instead of evidence.

This article explains why evidence collection matters and how to gather useful information before troubleshooting begins.

---

# The Cost of Missing Evidence

When evidence is incomplete, investigations often follow a familiar pattern:

1. An issue is reported
2. A likely system is blamed
3. Teams investigate based on assumptions
4. Escalations occur quickly
5. Root cause is discovered later in a different layer

This creates:

- unnecessary escalations
- delayed resolution
- duplicated effort
- frustration between teams
- incomplete troubleshooting history

In multi-layer environments, assumptions are expensive.

Modern web applications involve:

- clients
- WAFs
- origin infrastructure
- application layers
- external integrations

Failures may occur anywhere along the request path.

Without evidence, teams are often troubleshooting reputation rather than reality.

---

# Start With What Already Exists

Before running new tests or escalating issues, review the information already available.

Useful evidence may already exist.

Examples include:

- screenshots
- timestamps
- URLs
- HAR files
- raw HTTP requests and responses
- browser developer tools output
- WAF event IDs
- application logs
- proxy logs
- reproduction steps
- source IP information

The first goal is simple:

> Understand what is already known.

This aligns with:

→ [Step 00: Intake and Evidence Review](../playbooks/00-intake-and-evidence.md)

---

# Treat Second-Hand Information Carefully

Troubleshooting often begins with summaries such as:

- “The WAF is blocking it.”
- “The application team confirmed it isn’t the app.”
- “Networking ruled out routing.”
- “AI said the WAF could cause this.”

These statements may be useful.

But they are not evidence.

They should be treated as:

> leads, not conclusions.

Second-hand summaries often:

- omit context
- compress technical details
- remove timestamps
- hide uncertainty
- introduce interpretation errors

Always return to the underlying evidence.

---

# Evidence Should Match the Question

Different troubleshooting questions require different evidence.

The goal is not to collect everything.

The goal is to collect evidence relevant to the layer being investigated.

Examples:

| Question | Useful Evidence |
|---|---|
| Did the request traverse the WAF? | HAR files, HTTP headers, WAF logs |
| Did the hostname resolve correctly? | `dig`, `nslookup`, DNS results |
| Did traffic reach origin infrastructure? | proxy/LB logs, server logs |
| Did the application generate the response? | application logs, stack traces |

This prevents a common failure mode:

> Investigating a layer without evidence that the layer was involved.

---

# HAR Files and Raw HTTP Responses Are Often High-Value Evidence

One of the most useful troubleshooting artifacts is a HAR file or raw HTTP response.

These frequently contain:

- request URLs
- response codes
- timing information
- headers
- redirects
- cookies
- WAF fingerprints
- proxy indicators

In many cases, HAR files or raw responses can immediately help determine whether the request traversed the WAF.

Examples may include:

- WAF response headers
- vendor fingerprints
- proxy identifiers
- request behavior consistent with WAF handling

This makes HAR files particularly valuable during early troubleshooting.

DNS and routing analysis may still be needed, especially when investigating bypass conditions or explaining request path behavior.

But direct request evidence is often the fastest place to begin.

---

# Gather Evidence Before Escalating

Escalation is sometimes necessary.

But escalation without evidence usually increases confusion rather than reducing it.

Before escalating:

Collect:

- timestamps
- affected URLs
- reproduction steps
- request/response data
- logs
- relevant screenshots
- available identifiers

A good escalation package should allow the next team to answer:

- What happened?
- When did it happen?
- What evidence supports the report?
- Which layers are known to be involved?
- Which layers remain unverified?

This improves both speed and troubleshooting quality.

---

# Evidence Before Conclusions

Effective troubleshooting does not begin with blame.

It begins with evidence.

The purpose of evidence collection is not to slow troubleshooting.

It is to avoid wasting time investigating the wrong systems.

Whether using traditional troubleshooting methods or AI-assisted analysis, the principle remains the same:

> Evidence should guide the investigation.

Not assumptions.

Not reputation.

And not convenience.

---

# Related Content

- [Step 00: Intake and Evidence Review](../playbooks/00-intake-and-evidence.md)
- [Step 01: Verify Request Traverses the WAF](../playbooks/01-verify-client-points-to-waf.md)
- [AI-Assisted Troubleshooting](../ai/README.md)