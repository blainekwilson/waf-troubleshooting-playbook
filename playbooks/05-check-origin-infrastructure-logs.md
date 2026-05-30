# Step 05 – Check Origin Infrastructure Logs

## Purpose

Step 04 confirmed that the request traversed the WAF and determined how the WAF handled it.

At this point:

- WAF traversal has been confirmed
- WAF handling has been reviewed
- evidence suggests the request did not reach the API or web application

Step 05 focuses on the systems between the WAF and the application.

The objective is to determine:

- Did the request reach origin infrastructure?
- Which infrastructure component handled the request?
- Was the request forwarded successfully?
- Did infrastructure block, redirect, modify, or terminate the request?
- Where did the request stop?

This step helps isolate failures occurring between the WAF and the application layer.

---

# Preconditions

Before beginning Step 05:

- Step 03 should confirm WAF traversal
- Step 04 should confirm WAF handling
- timestamps should be collected
- hostname and URL should be known
- client public IP should be available
- WAF evidence should already be reviewed

Useful supporting evidence includes:

- HAR files
- raw HTTP requests and responses
- WAF logs
- request IDs
- screenshots
- reproduction steps

If WAF handling has not been confirmed, return to:

→ Step 04 – Confirm WAF Handling

---

# Understand the Origin Infrastructure Layer

Origin infrastructure refers to systems located between the WAF and the application.

Examples may include:

- firewalls
- load balancers
- reverse proxies
- ingress controllers
- web servers
- application servers
- service gateways
- routing infrastructure

Not every environment contains all of these systems.

The objective is to identify which infrastructure components participated in handling the request.

---

# Validate Time Synchronization First

Time alignment is critical.

A common troubleshooting failure occurs when logs use:

- different time zones
- unsynchronized clocks
- unknown offsets

Before comparing logs, determine:

- which time zone each system uses
- whether systems synchronize to a time server
- whether offsets exist between systems

Questions to answer:

- Are WAF logs UTC?
- Are infrastructure logs local time?
- Is daylight savings involved?
- Are devices synchronized using NTP or another time source?
- Has clock drift been identified?

If systems are not synchronized, establish the offset.

Example:

text id="8u0uij" WAF logs: 14:05 UTC Load balancer logs: 10:05 EST 

or:

text id="g6x1sy" WAF logs ahead by 90 seconds 

Without time normalization, valid events may appear unrelated.

Always normalize timestamps before correlation.

---

# Identify Relevant Infrastructure Components

Determine which systems should have handled the request.

Typical path examples:

text id="hmcq55" WAF → Load Balancer → Web Server → Application Server 

or:

text id="lh4ydo" WAF → Reverse Proxy → Application Server 

or:

text id="s7dcbm" WAF → Firewall → Load Balancer → Reverse Proxy → Application 

Map the expected path before reviewing logs.

Questions:

- Which systems received traffic from the WAF?
- Which systems should have forwarded traffic?
- Which systems could terminate or reject the request?

Understanding expected flow improves log correlation.

---

# Search Infrastructure Logs

Once the infrastructure path is understood, search logs for the request.

Common search criteria include:

- timestamp
- client public IP
- WAF source IP
- hostname
- URL or path
- request ID
- correlation ID
- response code

Examples:

- search logs during the affected timeframe
- search by WAF source IP
- search by URL and hostname
- correlate using request identifiers when available

Refer to your logging platform documentation for:

- search syntax
- query methods
- filtering options

Log structures vary significantly between vendors and platforms.

Refer to vendor documentation for:

- log formats
- field meanings
- correlation identifiers
- event interpretation

The objective is not merely finding logs.

The objective is determining how infrastructure handled the request.

---

# Determine Infrastructure Handling

Once matching events are located, determine how infrastructure handled the request.

Common outcomes may include:

- forwarded
- allowed
- redirected
- denied
- terminated
- modified
- timed out
- connection reset
- upstream unavailable

Questions:

- Did the infrastructure receive the request?
- Did it forward the request?
- Did it generate the response?
- Did the request terminate here?
- Was another upstream system contacted?

Do not assume infrastructure forwarded the request simply because it received it.

Receipt and successful forwarding are separate questions.

---

# If No Infrastructure Logs Exist

Sometimes infrastructure logging is disabled.

This creates a visibility gap.

If logging is unavailable:

- determine whether logging exists
- identify how logging is enabled
- determine log retention behavior
- understand performance and storage implications

Logging may need to be enabled temporarily for troubleshooting.

---

# Logging Storage and Retention Considerations

Enabling logging can generate large amounts of data.

Before enabling logs:

Understand:

- available drive space
- expected log growth
- retention settings
- overwrite behavior
- rotation policies

Many systems support:

- rolling logs
- log rotation
- overwrite policies
- capped storage

These settings help prevent:

- disk exhaustion
- service disruption
- infrastructure instability

However:

logs may also be overwritten quickly.

When enabling temporary logging:

- monitor storage consumption
- understand retention duration
- capture needed evidence promptly

Waiting too long may result in losing the relevant events.

---

# Determine Where the Request Stopped

The objective of Step 05 is identifying where the request stopped.

Possible findings include:

## Request Never Reached Infrastructure

Possible causes:

- WAF forwarding problem
- routing issue
- source restrictions
- network path failure

Return to:

→ Step 04 – Confirm WAF Handling

---

## Request Reached Infrastructure But Was Not Forwarded

Possible causes:

- firewall policy
- load balancer configuration
- reverse proxy behavior
- TLS mismatch
- infrastructure-generated response

Continue investigating infrastructure ownership.

---

## Request Was Forwarded Successfully

If logs confirm forwarding:

- request reached downstream systems
- infrastructure likely is not the stopping point

Proceed to:

→ Step 06 – Check Application and API Logs

---

# Common Troubleshooting Mistakes

Avoid:

- comparing unsynchronized logs
- assuming time zones match
- assuming receipt equals forwarding
- enabling logs without considering storage impact
- collecting logs without mapping request flow
- skipping intermediate infrastructure

Infrastructure troubleshooting is often a correlation exercise.

Successful investigations depend on:

- time normalization
- accurate path mapping
- disciplined log review

---

# Core Principle

> Infrastructure logs help determine where the request stopped.

Do not assume:

- infrastructure forwarded the request
- infrastructure blocked the request
- infrastructure is uninvolved

Use:

- synchronized timestamps
- request correlation
- infrastructure telemetry
- authoritative logs

to determine how origin infrastructure handled the request.

---

## Next Step

After checking origin infrastructure logs, proceed to:

[Step 06 – Check Application and API Logs](06-check-application-logs.md)

---

# Related Content

- Step 04 – Confirm WAF Handling
- Step 06 – Check Application and API Logs
- AI Guidance – Evidence Requirements
- AI Guidance – Authoritative Sources