## What this repo is

A collection of practical guides and playbooks for troubleshooting web applications behind WAFs.

Modern web applications span multiple layers:
- WAF (e.g., Imperva CloudWAF)
- Firewalls
- Load balancers / reverse proxies
- Web servers (IIS, NGINX, etc.)
- Application frameworks (Flask, .NET, etc.)

Issues are often attributed to the WAF but originate elsewhere or result from cross-layer misconfigurations.

## What you'll find here

- Articles: Deep dives into real troubleshooting scenarios
- Playbooks: Step-by-step debugging workflows
- Tools: Supporting utilities (e.g., log retrieval)
- Templates: Reusable checklists and workflows
- Examples: Sample logs and data for learning

## Project Status

This repository is actively being developed.

Current focus:
- Intake and evidence collection
- DNS and request-path validation
- WAF visibility verification

Future topics:
- IIS and FREB correlation
- Load balancer troubleshooting
- Flask application troubleshooting
- Header forwarding and TLS issues

## Core principle

**Trace the request across every layer.**

![Diagram showing a typical data flow through a WAF](diagrams/00-troubleshooting-flow.png)

## Start Here

- [Troubleshooting Methodology](playbooks/00-troubleshooting-methodology.md)

- [Step 00: Intake and Evidence Review](playbooks/00-intake-and-evidence.md)

- [Step 01: Verify the client is pointing to the WAF](playbooks/01-verify-client-points-to-waf.md)
