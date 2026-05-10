# Required Participants

WAF troubleshooting often crosses multiple ownership boundaries.

Make sure the correct technical owners are involved early.

## Common roles

| Layer | Who should be involved |
|---|---|
| Request / business impact | Requestor |
| Application behavior | Application owner or developer |
| DNS | DNS administrator |
| WAF | WAF administrator |
| Firewall / routing | Network or firewall engineer |
| Load balancer | Load balancer administrator |
| Web server | IIS / NGINX / Apache administrator |
| API gateway | API platform owner |
| Third-party integration | External technical contact |

## Why this matters

Incorrect or second-hand information can delay troubleshooting.

Examples:

- A non-technical user reports that “the WAF is blocking traffic”
- A support team relays information from another team without logs
- A team interprets an error message instead of sharing the original response
- A system owner assumes traffic path without validating it

Use participants to validate facts, not just provide opinions.