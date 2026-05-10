# Step 01: Verify the Client is Pointing to the WAF

## Goal

Confirm the client is resolving to the WAF, not bypassing it.

![Diagram showing a WAF bypass](../diagrams/01-client-bypass-flow.png)

## Before Troubleshooting

Review the available evidence first.

- [Step 00: Intake and Evidence Review](00-intake-and-evidence.md)
- [Authoritative Sources](../guides/00-intake-and-evidence/authoritative-sources.md)
- [Required Participants](../guides/00-intake-and-evidence/required-participants.md)

## What to check

- DNS resolution points to WAF IPs
- No hardcoded IPs in application or client
- No hosts file overrides
- Split DNS is not bypassing the WAF
- Server-to-server traffic is understood and documented
- Rogue or unmanaged APIs are identified

## How to verify

- [Step 02: Verify the request reaches the WAF](02-verify-request-reaches-waf.md).
