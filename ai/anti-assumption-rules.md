# Anti-Assumption Rules for AI-Assisted Troubleshooting

AI systems can unintentionally reinforce assumptions when prompts contain incomplete or biased information.

These rules are intended to reduce assumption amplification during troubleshooting.

---

# Core Principle

> Plausibility is not proof.

---

## Rule: Possible Is Not Probable

If a user asks whether the WAF could cause a symptom, first identify common non-WAF causes.

Example:

For HTTP 426, consider likely causes such as:

- protocol upgrade requirements
- HTTP version negotiation
- TLS/proxy behavior
- origin server configuration
- application or framework behavior

Only then evaluate where the WAF could fit.

The AI should distinguish between:

- possible
- likely
- proven
- disproven

---

# Rules

## 1. Do Not Assume the WAF Handled the Request

Never assume traffic traversed the WAF unless evidence confirms it.

Validate:

- DNS resolution
- request path
- WAF logs
- network flow

before analyzing WAF policy behavior.

---

## 2. Treat Second-Hand Information as Unverified

Statements such as:

- “The application team confirmed it”
- “The network team ruled that out”
- “AI said it was likely”
- “The screenshot shows…”

should be treated as leads, not authoritative evidence.

---

## 3. Require Layer-Specific Evidence

Each troubleshooting layer should have its own evidence source.

Examples:

- DNS → `dig`, `nslookup`
- WAF → WAF logs
- Application → application logs
- TLS → LB/web server logs

---

## 4. Do Not Reinforce Hypotheses Without Evidence

Avoid responses such as:

> “Yes, the WAF could definitely cause this.”

without evidence that:
- traffic traversed the WAF
- the WAF generated the response
- the WAF policy evaluated the request

---

## 5. Identify Multiple Possible Causes

When evidence is incomplete, identify possible explanations instead of selecting a preferred explanation.

Example:

- split DNS
- direct-to-origin traffic
- WAF policy
- application authorization logic
- proxy behavior

---

## 6. Validate Request Flow Sequentially

Troubleshooting should follow request flow order:

1. Intake and evidence review
2. Verify requestor points to WAF
3. Verify request reaches WAF
4. Confirm WAF handling
5. Validate forwarding
6. Check origin behavior

---

# Related Content

- [Authoritative Sources](authoritative-sources.md)
- [Example Prompts](example-prompts.md)