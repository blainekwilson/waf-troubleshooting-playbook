# Step 00: Intake and Evidence Review

Before troubleshooting any reported WAF issue, review the information already collected and validate the quality of that information.

Many WAF investigations are delayed because teams begin troubleshooting from assumptions, second-hand explanations, or interpreted summaries instead of direct evidence.

## Goal

Establish what is known, what has been validated, who provided the information, and what evidence is still missing.

## What to collect first

Ask the requestor for any existing evidence, including:

- Description of the issue
- Exact URL or endpoint
- Date, time, and timezone of the issue
- Source IP address or client location
- Screenshots
- Error messages
- HAR files
- HTTP request and response examples
- WAF event IDs
- DNS lookup results
- Application logs
- Web server logs
- Load balancer logs
- Firewall logs
- Packet captures, if available

## Validate the information source

Not all information has the same reliability.

Prioritize:

1. Direct logs from the system of record
2. Raw request/response data
3. Screenshots showing exact errors
4. Output from commands run during the issue
5. First-hand explanation from the technical owner
6. Second-hand or interpreted summaries

Be careful with statements like:

- “The WAF is blocking it”
- “The request is failing at the WAF”
- “The app team confirmed it is not the application”
- “Networking said everything is open”

These may be true, but they need supporting evidence.

## Required participants

Identify who needs to be involved based on the suspected layer.

Common participants include:

| Area | Role / Owner |
|---|---|
| Request details | Requestor or application owner |
| DNS / resolution | DNS administrator or platform owner |
| WAF | WAF administrator |
| Firewall / routing | Network or firewall engineer |
| Load balancer | Load balancer administrator |
| Web server | IIS / NGINX / Apache administrator |
| Application | Application owner or developer |
| External integration | Third-party technical contact |

## Why this matters

Troubleshooting WAF issues can quickly overwhelm junior staff because the investigation often crosses multiple layers and teams.

A structured intake process helps junior analysts:

- Avoid chasing assumptions
- Identify missing evidence
- Know who to engage
- Escalate with useful context
- Reduce unnecessary senior-engineer involvement

## Next step

After intake is complete, proceed to:

[Step 01: Verify the client is pointing to the WAF](01-verify-client-points-to-waf.md)