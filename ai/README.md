# AI-Assisted WAF Troubleshooting

AI tools can help accelerate troubleshooting, summarize evidence, and assist with analysis.

However, AI systems can also reinforce incorrect assumptions when prompts contain incomplete, inaccurate, or second-hand information.

This section provides guidance for using AI tools during WAF and web application troubleshooting.

The goal is not to replace technical troubleshooting methodology with AI.

The goal is to ensure AI-assisted troubleshooting remains:

- evidence-driven
- layer-aware
- operationally accurate
- resistant to assumption amplification

---

## Common Failure Modes

Examples of problematic AI-assisted troubleshooting include:

- Assuming the WAF handled a request without evidence
- Reinforcing unsupported conclusions
- Treating second-hand information as authoritative
- Skipping request flow validation
- Jumping directly to WAF rule analysis before confirming traffic traversed the WAF

---

## Core Principle

> AI should assist troubleshooting methodology — not replace it.

Always validate claims using authoritative technical evidence.

---

## Related Playbooks

- [Step 00: Intake and Evidence Review](../playbooks/00-intake-and-evidence.md)
- [Step 01: Verify the Client is Pointing to the WAF](../playbooks/01-verify-client-points-to-waf.md)
- [Step 02: Verify the Request Reaches the WAF](../playbooks/02-verify-request-reaches-waf.md)

---

## Files in this Section

- [Authoritative Sources](authoritative-sources.md)
- [Anti-Assumption Rules](anti-assumption-rules.md)
- [Evidence-Driven Troubleshooting](evidence-driven-troubleshooting.md)
- [Example Prompts](example-prompts.md)
- [Troubleshooting Skill / AI Instructions](troubleshooting-skill.md)