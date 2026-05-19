# Evidence Requirements

AI-assisted troubleshooting should request evidence appropriate to the layer being investigated.

---

# Core Principle

> Troubleshooting conclusions should be constrained by evidence.

If evidence is missing, identify the missing evidence before evaluating root cause.

---

# Step 00 — Intake and Evidence Review

Request:

- timestamps
- screenshots
- HAR files
- request/response samples
- affected URLs
- source IPs
- reproduction steps

---

# Step 01 — Verify Requestor Traverses the WAF

Preferred evidence:

- HAR files
- raw HTTP requests/responses
- WAF response headers
- WAF fingerprints
- matching WAF logs

Supporting evidence:

- DNS (`dig`, `nslookup`)
- internal vs external resolution
- hardcoded IP validation

---

# Step 02 — Verify Request Reaches WAF

Request:

- WAF logs
- request timestamps
- source IP
- correlation IDs
- event IDs

---

# Step 03 — Confirm WAF Handling

Request:

- WAF action logs
- response codes
- policy/rule identifiers
- response fingerprints

---

# Origin Infrastructure

Request:

- load balancer logs
- proxy logs
- web server logs
- TLS negotiation evidence

---

# Application Layer

Request:

- application logs
- framework logs
- authorization failures
- stack traces
- API responses