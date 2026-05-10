# Junior Triage Guidance

WAF issues can become complex quickly because they often involve DNS, routing, WAF policy, firewall rules, load balancers, web servers, and application behavior.

This guide helps junior analysts collect useful information before escalation.

## Junior analyst goals

Before escalating, collect:

- What is failing?
- Who is affected?
- When did it fail?
- What URL or endpoint is involved?
- What error was observed?
- Is there a screenshot or HAR file?
- What source IP was used?
- Has DNS resolution been checked?
- Is there evidence the request reached the WAF?
- Are there WAF event IDs or access logs?

## Escalate when

Escalate to senior staff when:

- The requestor cannot provide enough detail
- Multiple teams disagree on the traffic path
- Logs conflict across layers
- The issue involves production impact
- A WAF rule change may be required
- A bypass or unprotected API is suspected
- Firewall, routing, or load balancer ownership is unclear

## Escalation summary format

Use this format when escalating:

```text
Issue:
Affected URL / endpoint:
Requestor:
Time of issue:
Source IP / location:
Evidence collected:
What has been validated:
What is still unknown:
Teams already engaged:
Reason for escalation: