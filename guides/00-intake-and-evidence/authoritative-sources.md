# Authoritative Sources for Troubleshooting Data

During WAF troubleshooting, different teams may provide different interpretations of the issue.

Use the most authoritative source available for each type of data.

| Data Needed | Preferred Authoritative Source |
|---|---|
| Exact user-facing error | Screenshot, browser developer tools, HAR file |
| Exact request URL | HAR file, browser developer tools, application logs |
| HTTP request headers | HAR file, packet capture, WAF logs |
| HTTP response code | WAF logs, web server logs, HAR file |
| DNS resolution | `nslookup`, `dig`, DNS admin tools |
| Whether traffic reached the WAF | WAF access logs or event logs |
| Whether WAF blocked traffic | WAF security event logs |
| Whether traffic reached origin | Web server logs, application logs, load balancer logs |
| Firewall allow/block decision | Firewall logs |
| Load balancer routing decision | Load balancer logs |
| Application behavior | Application logs and application owner validation |

## Guidance

Prefer raw evidence over interpreted summaries.

For example:

- Prefer a HAR file over “the browser got an error”
- Prefer WAF logs over “the WAF blocked it”
- Prefer IIS logs over “the server never received it”
- Prefer firewall logs over “the port is open”

The goal is not to distrust people. The goal is to avoid troubleshooting based on incomplete or interpreted information.