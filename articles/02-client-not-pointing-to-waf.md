# 10% of “WAF Issues” Never Reach the WAF

I track WAF support and troubleshooting tickets each month.  Last month, approximately **10% of reported “WAF issues” had nothing to do with the WAF at all**.  In these cases, the traffic never passed through the WAF.

Modern web application troubleshooting is difficult because requests traverse multiple independently managed layers:

- DNS
- WAFs
- Firewalls
- Load balancers
- Web servers
- Application frameworks
- External integrations

In many environments:
- Teams only understand their own layer
- Evidence is incomplete or second-hand
- Troubleshooting escalates quickly to senior engineers
- The WAF often becomes the default system blamed for failures

This project exists to provide a structured troubleshooting methodology and the methodology is organized into numbered troubleshooting steps that follow the request path across the environment to help teams:

- Collect better evidence
- Identify the correct technical owners
- Validate assumptions
- Trace requests across layers
- Reduce unnecessary escalations

Before reviewing logs, tuning rules, or investigating false positives, there is one critical question that must be answered:

> **Is the client pointing to the WAF at all?**

If the answer is no, everything else is a distraction.

![Diagram showing traffic bypassing the WAF](../diagrams/01-client-bypass-flow.png)

---

## Before Troubleshooting: Review the Evidence

Before starting Step 01, review what the requestor has already collected.

This may include:

- Screenshots
- Error messages
- HAR files
- HTTP requests and responses
- DNS lookup results
- WAF event IDs
- Web server logs
- Application logs

Do not rely only on second-hand summaries such as “the WAF is blocking it” or “the application team confirmed it is not the app.”  Those statements may be accurate, but they should be treated as leads, not conclusions.

Start with the evidence.

→ See: [Step 00: Intake and Evidence Review](../playbooks/00-intake-and-evidence.md)

---

## Step 01: Verify the Client is Pointing to the WAF

This is the first technical validation step in the troubleshooting methodology.

If this step is skipped, it’s easy to:
- Misattribute issues to the WAF  
- Waste time analyzing logs that don’t exist  
- Miss gaps in architecture or onboarding  

---

## Common Ways Traffic Bypasses the WAF

In modern environments, there are multiple ways for traffic to bypass the WAF entirely.

### 1. Split DNS (Internal Bypass)

Internal users may resolve the application hostname to an internal/private IP instead of the WAF.

Result:
- Traffic never leaves the network  
- Requests go directly to the origin server  
- The WAF is completely bypassed  
- WAF logs will not exist  

Example:

An internal user reported that the WAF was blocking requests to an application.

Investigation showed:
- Internal DNS resolved directly to the origin server
- Traffic never traversed the WAF
- No WAF logs existed for the request

The issue was caused by split DNS configuration, not WAF policy.

---

### 2. Server-to-Server Communication

Backend systems often communicate directly with application servers.

This may be:
- intentional (performance, internal trust)  
- undocumented (legacy behavior)  

Either way:
- Traffic does not traverse the WAF  
- WAF logs will not exist  

---

### 3. Rogue or Unmanaged APIs

New services or APIs may be deployed without being onboarded to the WAF.

This creates:
- Visibility gaps  
- Security gaps  
- Inconsistent behavior across endpoints  
- WAF logs will not exist  

---

### 4. Third-Party Integrations

Applications often communicate with external services that do not traverse the WAF.

Support teams may incorrectly assume:
- all HTTP/S traffic passes through the WAF
- outbound application requests are visible in WAF logs

In many environments, outbound traffic traverses separate proxy or egress infrastructure, not the WAF.

Result:
- WAF logs will not exist
- Troubleshooting must shift to the appropriate outbound security or network layer

---

## How to Quickly Verify the Client is Pointing to the WAF

Before going deeper, validate that the client is actually pointing to the WAF.

At a high level:

- Resolve the application hostname (e.g., `nslookup`, `dig`)
- Confirm the resolved IP matches the WAF
- Check for internal vs external DNS differences
- Ensure no hardcoded IPs are being used
- Validate the client is not connecting directly to the origin

→ See: [Step 01: Playbook](../playbooks/02-verify-client-points-to-waf.md)

---

## Why This Step Matters

If the client is not pointing to the WAF:

- There will be **no WAF logs**
- No WAF rules will be evaluated
- No blocking or filtering can occur

Yet these scenarios are often reported as:
- “WAF is blocking traffic”
- “WAF is not allowing requests”
- “WAF is causing errors”

In reality, the WAF is not involved at all.

---

## Key Takeaway

> **If you cannot prove the client is pointing to the WAF, you are troubleshooting the wrong layer.**

Always start with Step 01.

---

## What’s Next

Once you’ve confirmed the client is pointing to the WAF, the next step is to determine if the traffic reached the WAF.

→ See: [Step 02: Verify the Request Reaches the WAF](../playbooks/02-verify-request-reaches-waf.md)