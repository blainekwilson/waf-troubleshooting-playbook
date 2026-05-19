# Troubleshooting Methodology

The playbooks in this repository follow the flow of a request through a modern web application stack.

The goal is to avoid guessing where a “WAF issue” is occurring and instead prove each layer one step at a time.

## Core principle

> Trace the request across every layer.

## Troubleshooting steps

- Step 01: [Intake and Evidence Review](01-intake-and-evidence.md)
- Step 02: [Verify the client is pointing to the WAF](02-verify-client-points-to-waf.md)
- Step 03: [Verify the request reaches the WAF](03-verify-request-reaches-waf.md)
- Step 04: [Confirm WAF handling](04-confirm-waf-handling.md)
- Step 05: Check Origin Infrastructure logs
- Step 06: Check API/application logs
- Step 07: Compare response codes across layers

## Why Step 00 exists

Many investigations fail before technical troubleshooting begins.

Common causes include:

- Missing evidence
- Second-hand information
- Non-technical interpretation of technical errors
- Incorrect assumptions about ownership
- The wrong teams being involved

Step 01 exists to establish the facts before troubleshooting the flow.