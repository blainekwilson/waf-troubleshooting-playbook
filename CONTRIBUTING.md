# Contributing to the WAF Troubleshooting Playbook

Thank you for your interest in contributing! This repository is a community resource for engineers who troubleshoot web applications behind WAFs. Contributions of all kinds are welcome — new playbooks, corrections, real-world scenarios, diagrams, and tooling improvements.

---

## Table of Contents

- [Who Should Contribute](#who-should-contribute)
- [What We Need](#what-we-need)
- [Repository Structure](#repository-structure)
- [Playbook Format](#playbook-format)
- [Article Format](#article-format)
- [Contribution Workflow](#contribution-workflow)
- [Quality Standards](#quality-standards)
- [Vendor-Specific Content](#vendor-specific-content)
- [Diagrams](#diagrams)
- [Reporting Issues](#reporting-issues)

---

## Who Should Contribute

This repo is for practitioners — security engineers, network engineers, sysadmins, developers, and support professionals who have hands-on experience troubleshooting real WAF issues. You do not need to be an expert in every WAF vendor to contribute; focused, accurate knowledge of one layer or one vendor is valuable.

---

## What We Need

Contributions are welcome in any of the following areas:

- **Playbooks** — Step-by-step troubleshooting workflows for a specific layer or problem class
- **Guides** — Detailed reference material supporting a playbook step (e.g., how to read a specific log format)
- **Articles** — Write-ups of real troubleshooting scenarios, including what was tried, what the evidence showed, and what the root cause was
- **Templates** — Reusable checklists, intake forms, or ticket templates
- **Diagrams** — Architecture or flow diagrams illustrating request paths, bypass scenarios, or log correlation
- **Tools** — Scripts or utilities that support the troubleshooting process (log retrieval, DNS checks, etc.)
- **Corrections** — Fixes for inaccurate commands, outdated information, or broken links

---

## Repository Structure

```
waf-troubleshooting-playbook/
├── playbooks/          # Step-by-step troubleshooting workflows
├── guides/             # Reference material supporting playbook steps
├── articles/           # Real-world troubleshooting scenarios
├── templates/          # Reusable checklists and intake forms
├── diagrams/           # Architecture and flow diagrams
├── tools/              # Supporting scripts and utilities
└── .github/            # Issue templates and repo configuration
```

---

## Playbook Format

Playbooks follow a consistent structure so readers can navigate them predictably. Use the format below as your starting point.

```markdown
# Step XX: [Title]

## Goal

One or two sentences describing what this step confirms or rules out.

## Before Troubleshooting

List any prerequisite steps or evidence that should be reviewed first.

## What to Check

A list of specific conditions, configurations, or behaviors to examine.

## How to Verify

Concrete commands, log queries, or UI steps to confirm each check.
Include the expected output and what a failure looks like.

## Next Step

Link to the next playbook step, or describe the decision branch
(e.g., "If WAF logs show the request, proceed to Step 03. If not, see...").
```

**Guidelines for playbook content:**

- Be specific. Include actual commands, field names, and example output where possible.
- Distinguish between what to check and how to verify — the "what" is the diagnostic question, the "how" is the method.
- Note WAF-vendor-specific steps explicitly (see [Vendor-Specific Content](#vendor-specific-content)).
- Avoid assumptions about the reader's access level — note when elevated permissions or vendor portal access is required.
- Name files using the pattern `NN-short-descriptive-name.md` (e.g., `03-confirm-waf-handling.md`).

---

## Article Format

Articles document real troubleshooting scenarios. They are not step-by-step workflows — they are narratives that show how a problem was found and resolved.

```markdown
# [Descriptive Title of the Scenario]

## Summary

One paragraph describing the problem, environment, and outcome.

## Environment

- WAF vendor and mode (e.g., Imperva CloudWAF, reverse proxy)
- Origin server type (e.g., IIS 10, NGINX)
- Application framework if relevant (e.g., Flask, .NET)

## Symptoms

What was reported and by whom. Include HTTP status codes, error messages,
and how the problem was first described.

## Investigation

Chronological account of the troubleshooting steps taken, evidence collected,
and hypotheses that were ruled out.

## Root Cause

What the problem actually was.

## Resolution

What was changed or configured to fix it.

## Lessons Learned

What this scenario illustrates about WAF troubleshooting methodology.
```

Anonymize customer or employer details. Sanitize any sensitive data in log examples.

---

## Contribution Workflow

1. **Open an issue first** for new playbooks or articles, using the relevant issue template. This avoids duplicate effort and lets maintainers give early feedback on scope.
2. **Fork the repository** and create a branch named descriptively (e.g., `add-playbook-origin-logs` or `fix-step01-dns-commands`).
3. **Write your content** following the format guidelines above.
4. **Submit a pull request** with a clear description of what was added or changed and why.
5. A maintainer will review and may request clarifications or adjustments before merging.

For small corrections (typos, broken links, outdated commands), you can skip the issue and submit a PR directly.

---

## Quality Standards

- **Accuracy over completeness.** If you are not confident about a specific command or behavior, note it as unverified or omit it.
- **Reproducible steps.** Commands and verification steps should work as written. If the output varies by environment, say so.
- **Vendor attribution.** When a step is specific to one WAF vendor or platform, label it clearly.
- **No marketing language.** This is a technical resource. Avoid vendor promotional framing.
- **Plain language.** Write for a competent engineer who may be unfamiliar with this specific layer or vendor.

---

## Vendor-Specific Content

This repository is vendor-agnostic in methodology but vendor-specific in implementation details. When contributing vendor-specific content:

- Label it clearly at the top of the section (e.g., `> **Imperva CloudWAF**` or `> **AWS WAF**`).
- Place vendor-specific guides in `guides/<step-name>/<vendor>/` to keep them organized.
- Do not assume the reader uses the same vendor across all layers — origin servers, load balancers, and WAFs are often from different vendors.

Currently documented vendors include Imperva CloudWAF. Contributions covering Cloudflare, AWS WAF, Azure Front Door, Akamai, F5, Fastly, and others are welcome.

---

## Diagrams

Diagrams are stored in the `diagrams/` folder as PNG files. If you are contributing a diagram:

- Use clear, high-contrast styling legible at standard screen resolution.
- Include the source file (e.g., `.drawio`, `.excalidraw`) if possible so others can update it.
- Name files to match the playbook step they support (e.g., `01-client-bypass-flow.png`).

---

## Reporting Issues

Use the GitHub issue templates to report:

- Inaccuracies or outdated information
- Missing steps or gaps in a playbook
- Real-world scenarios worth documenting
- Suggestions for new playbook topics

For security-sensitive issues, please open a regular issue — this repository contains no production systems or credentials.

---

Thank you for helping build a resource that makes WAF troubleshooting less painful for everyone.
