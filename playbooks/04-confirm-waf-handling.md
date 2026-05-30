# Step 04 – Confirm WAF Handling

Purpose

Step 03 confirmed whether the request traversed the WAF.

Step 04 focuses on determining how the WAF handled the request.

This step answers questions such as:

* Did the WAF see the request?
* How did the WAF evaluate the request?
* Did the WAF allow, challenge, modify, or block the request?
* Did the WAF generate the response?
* Was the request forwarded to origin infrastructure?

The goal is to determine WAF handling behavior using authoritative evidence.

⸻

Preconditions

Before beginning Step 04:

* Step 03 should confirm or strongly suggest WAF traversal
* timestamps should be available
* hostname and affected URL should be known
* client information should be collected
* available evidence should already be reviewed

Examples of useful evidence:

* HAR files
* raw HTTP requests and responses
* screenshots
* request timestamps
* WAF headers or fingerprints
* reproduction steps

If WAF traversal has not been validated, return to:

→ Step 03 – Verify Request Traverses the WAF

⸻

Search WAF Logs

The next objective is locating the request within WAF telemetry.

Most WAF platforms provide:

* native log search
* SIEM integration
* API access
* event search tools
* request correlation features

Common search criteria include:

* timestamp
* client public IP address
* hostname
* URL or path
* request ID
* correlation ID
* response code

Examples:

* search events within the affected timeframe
* search by client IP
* search by hostname and path
* correlate with request identifiers when available

Refer to your SIEM or logging platform documentation for query syntax and search methods.

⸻

Understand WAF Handling Outcome

Once the request is located, determine how the WAF handled it.

Most WAF platforms provide some indication of request disposition or handling outcome.

Common handling categories may include:

* Allowed
* Blocked
* Challenged
* Rate limited
* Redirected
* Modified
* Logged only
* Forwarded to origin

Each WAF vendor exposes handling details differently.

Refer to your WAF vendor documentation for:

* log structures
* field definitions
* event interpretation
* policy outcome indicators

The objective is not merely finding the request.

The objective is understanding how the WAF processed it.

⸻

Determine Response Ownership

A common troubleshooting challenge is determining who generated the response.

Possible ownership includes:

* WAF
* origin infrastructure
* application layer
* intermediary systems

Questions to answer:

* Did the WAF generate the response?
* Did the WAF forward the request?
* Did the request reach origin infrastructure?
* Did another system modify the response?

Helpful evidence includes:

* WAF logs
* WAF disposition fields
* response headers
* origin infrastructure logs
* application logs
* request correlation identifiers

Avoid assuming the WAF generated a response simply because the request traversed it.

Traversal and ownership are different questions.

⸻

Return to Step 03 When Needed

Some troubleshooting situations require returning to Step 03.

This is especially true when evidence suggests client compatibility or transport problems.

Return to Step 03 when:

* no matching WAF logs exist
* client behavior is inconsistent
* browser testing succeeds but application clients fail
* TLS negotiation appears incomplete
* certificate mismatch occurs
* WAF traversal remains uncertain
* legacy client compatibility is suspected
* non-SNI behavior is suspected
* TLS protocol or cipher limitations are suspected

Examples may include:

* healthcare applications using older client libraries
* legacy Java environments
* embedded or appliance-based clients
* applications with outdated TLS implementations

Legacy TLS and non-SNI testing are valuable when evidence suggests compatibility limitations.

They are not required for routine WAF handling validation.

⸻

Opening a WAF Vendor Support Case

Vendor support may be necessary when:

* WAF handling appears inconsistent
* WAF disposition is unclear
* unexpected behavior occurs
* suspected edge or proxy problems exist
* vendor-side investigation is required

Support cases are more effective when evidence is collected before escalation.

⸻

Required Information for Support Cases

Typical support requests require:

* affected hostname
* URL or endpoint
* timestamp
* response code
* client public IP address
* WAF proxy or edge information
* collected evidence
* screenshots or HAR files when available

The more precise the evidence, the faster vendor support can investigate.

⸻

Obtain the Client Public IP Address

This step is often overlooked.

Many users provide private IP addresses instead of Internet-facing addresses.

Private addresses are typically:

10.x.x.x
172.16–31.x.x
192.168.x.x

These are usually not useful for Internet troubleshooting.

Ask the client to identify their public Internet IP.

Common methods include:

Browser:

* https://ipchicken.com
* https://ifconfig.me
* https://whatismyip.com

Ask the client to provide:

* public IP address
* timestamp
* affected hostname

This information is frequently required for WAF log correlation and vendor support.

⸻

Identify WAF Proxy or Edge Information

Most WAF platforms provide some method for identifying:

* proxy server
* edge location
* POP
* request ID
* gateway identifier

This information is often useful during support escalation.

Examples:

Imperva

Look for:

* proxy IP
* gateway identifier
* support-visible proxy details
* request correlation information

Cloudflare

Look for:

* CF-Ray
* edge identifiers
* request correlation details

Akamai

Look for:

* edge hostname
* request ID
* correlation identifiers

AWS WAF

Correlate using:

* CloudWatch logs
* ALB or CloudFront identifiers
* request tracing

Azure Front Door / WAF

Look for:

* tracking IDs
* Front Door logs
* correlation identifiers

Refer to vendor documentation for platform-specific methods.

⸻

When to Open a Vendor Case

Consider vendor escalation when:

* WAF traversal is confirmed
* WAF handling is confirmed
* evidence remains inconsistent
* edge behavior appears abnormal
* WAF-generated behavior remains unexplained
* vendor-side networking or infrastructure is suspected

Avoid opening vendor cases before confirming:

* traversal
* timestamps
* public client IP
* collected evidence

Premature escalation often delays troubleshooting.

⸻

Escalation Checklist

Before escalation, confirm:

* affected hostname known
* affected URL known
* timestamp collected
* client public IP identified
* WAF traversal validated
* WAF logs searched
* HAR or HTTP evidence reviewed
* screenshots collected if applicable
* proxy or edge information identified
* competing explanations considered

Good escalation packages reduce investigation time and improve troubleshooting accuracy.

⸻

Core Principle

Confirming WAF handling requires evidence.

Do not assume:

* the WAF generated the response
* the WAF blocked the request
* the WAF is responsible

Use:

* telemetry
* logs
* request tracing
* authoritative evidence

to determine how the WAF actually handled the request.

⸻

## Next Step

After confirming WAF handling, proceed to:

[Step 05 – Check Origin Infrastructure Logs](05-check-origin-infrastructure-logs.md)

⸻

Related Content

* Step 03 – Verify Request Traverses the WAF
* Step 05 – Validate Forwarding to Origin
* AI Guidance – Evidence Requirements
* AI Guidance – Authoritative Sources