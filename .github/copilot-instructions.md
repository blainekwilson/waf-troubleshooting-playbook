# Copilot Instructions

This repository documents operational troubleshooting methodology for web applications behind WAFs.

## Terminology

- "Requestor" = human or team reporting the issue
- "Client" = browser, API client, or system making the HTTP request
- "Origin" = backend application or web server behind the WAF

## Repository structure

- `/playbooks` = step-by-step troubleshooting workflows
- `/guides` = detailed technical implementation guidance
- `/articles` = narrative or scenario-driven articles
- `/templates` = reusable operational templates
- `/diagrams` = workflow and architecture diagrams

## Troubleshooting philosophy

Always:
- Trace the request across every layer
- Validate assumptions with evidence
- Prefer authoritative sources over interpreted summaries
- Identify the correct technical owners early
- Avoid troubleshooting based on second-hand information

## Step numbering

- Step 00 = Intake and Evidence Review
- Step 01 = Verify the client is pointing to the WAF
- Step 02 = Verify the request reaches the WAF
- Step 03 = Confirm WAF handling
- Step 04 = Validate forwarding to origin
- Step 05 = Check origin logs
- Step 06 = Compare response codes across layers

## Style guidance

Prefer:
- concise operational language
- bullet points
- actionable troubleshooting guidance
- real-world examples

Avoid:
- marketing language
- exaggerated claims
- unnecessary buzzwords
- overly theoretical explanations