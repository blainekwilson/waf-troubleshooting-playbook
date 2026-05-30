# Step 06 – Check Application and API Logs

## Purpose

Step 05 confirmed that the request successfully traversed origin infrastructure.

At this point:

- WAF traversal has been confirmed
- WAF handling has been reviewed
- origin infrastructure has been evaluated
- evidence suggests the request reached the application layer

Step 06 focuses on application and API logging.

The objective is to determine:

- Did the application receive the request?
- How did the application process the request?
- Did the application generate the response?
- Did application logic reject or fail the request?
- Did the request terminate inside the application?

This step helps identify issues occurring within the application or API layer.

---

# Preconditions

Before beginning Step 06:

- Step 04 should confirm WAF handling
- Step 05 should confirm infrastructure forwarding
- timestamps should be collected
- hostname and URL should be known
- client public IP should be available
- supporting evidence should already be reviewed

Useful evidence includes:

- HAR files
- raw HTTP requests and responses
- WAF logs
- infrastructure logs
- screenshots
- request IDs
- reproduction steps

If origin infrastructure handling remains uncertain, return to:

→ Step 05 – Check Origin Infrastructure Logs

---

# Application Logging Expectations

Applications should generate logs capable of supporting troubleshooting, monitoring, and security investigations.

Application logging should follow established logging standards and secure development practices.

A commonly referenced standard is:

- OWASP Application Logging guidance

Applications should generally:

- record meaningful events
- include timestamps
- support request correlation
- provide useful error context
- avoid logging sensitive information unnecessarily

The purpose of application logging is not simply producing log files.

The purpose is enabling investigation and operational visibility.

---

# Use Established Logging Frameworks

Applications should generally use established logging frameworks rather than custom logging implementations.

Examples may include:

- log4j
- log4net
- structured logging libraries
- platform-native logging frameworks

Established frameworks typically provide:

- standardized formatting
- log rotation
- configurable verbosity
- centralized collection support
- correlation features
- operational consistency

Avoid relying solely on:

- console output
- ad hoc logging
- temporary debug statements
- custom logging without operational controls

Framework and implementation choices vary by language and platform.

Refer to your application stack documentation for framework-specific guidance.

---

# Validate Time Synchronization First

Time correlation remains critical.

Application logs often introduce additional timing complexity because:

- applications may use local time
- infrastructure may use UTC
- containers may differ from hosts
- clocks may drift
- distributed systems may have offsets

Before comparing logs, determine:

- application log time zone
- infrastructure log time zone
- whether systems synchronize to a time source
- whether offsets exist

Questions:

- Are logs UTC?
- Are logs local time?
- Are containers synchronized?
- Is daylight savings involved?
- Is NTP or another time source configured?

If systems are not synchronized:

establish the offset.

Examples:

text id="sv8m8l" Infrastructure logs: 14:05 UTC Application logs: 10:05 EST 

or:

text id="wt1r86" Application server behind by 45 seconds 

Without normalized timestamps, valid application events may appear unrelated.

Always normalize time before correlation.

---

# Search Application Logs

The next objective is locating the request inside application telemetry.

Common search criteria include:

- timestamp
- client public IP
- hostname
- URL or endpoint
- request ID
- correlation ID
- session ID
- username when appropriate
- response code
- application error identifiers

Examples:

- search by request timeframe
- search by endpoint
- search by correlation ID
- search by application error ID

Application logging platforms vary significantly.

Refer to your:

- logging platform
- APM tooling
- SIEM
- application framework documentation

for query syntax and search methods.

The objective is not simply finding entries.

The objective is understanding how the application processed the request.

---

# Determine Application Handling

Once relevant events are located, determine what the application did.

Common outcomes include:

- request processed successfully
- validation failure
- authentication failure
- authorization failure
- exception generated
- backend dependency failure
- timeout
- malformed request rejection
- application-generated response

Questions:

- Did the application receive the request?
- Did application logic process it?
- Did validation fail?
- Did an exception occur?
- Did the application generate the response?
- Did a downstream dependency fail?

Avoid assuming successful receipt equals successful processing.

Receipt and successful execution are different questions.

---

# Identify Application Ownership

Application issues may originate from multiple layers.

Possible ownership may include:

- application code
- API gateway
- middleware
- authentication systems
- backend services
- databases
- third-party integrations

Questions:

- Which component generated the error?
- Which component returned the response?
- Did the application fail internally?
- Did a dependency fail?

Correlation and ownership remain important.

Do not collapse multiple systems into a single conclusion without evidence.

---

# If Application Logging Is Missing

Some applications do not currently produce sufficient logs.

This creates a visibility gap.

If logging is unavailable:

determine:

- whether logging exists
- whether logging can be enabled
- what visibility is available
- what operational impact exists

Temporary logging may be required.

---

# Logging Storage and Retention Considerations

Enabling application logging may generate large volumes of data.

Before enabling logging:

understand:

- available disk space
- expected log growth
- retention settings
- overwrite behavior
- rotation policies
- performance implications

Most logging frameworks provide support for:

- log rotation
- rolling files
- overwrite behavior
- size limits
- retention policies

These features help prevent:

- disk exhaustion
- degraded application performance
- operational instability

However:

logs may also be overwritten quickly.

When enabling temporary logging:

- monitor storage usage
- understand retention limits
- collect evidence promptly

Waiting too long may result in losing the relevant events.

---

# Common Troubleshooting Mistakes

Avoid:

- comparing unsynchronized logs
- assuming timestamps align
- relying only on console output
- enabling logs without monitoring storage
- assuming receipt equals processing
- assuming the application generated the response without evidence
- ignoring downstream dependencies

Application troubleshooting is often a correlation exercise.

Successful investigations depend on:

- normalized timestamps
- disciplined log review
- correlation identifiers
- authoritative telemetry

---

# Determine Whether the Request Reached the Application

The primary objective of Step 06 is determining:

> Did the request reach and execute inside the application?

Possible findings include:

## Request Never Reached the Application

Possible causes:

- infrastructure forwarding issue
- routing failure
- middleware termination
- upstream rejection

Return to:

→ Step 05 – Check Origin Infrastructure Logs

---

## Request Reached the Application But Failed

Possible causes:

- validation failure
- authentication issue
- exception
- dependency outage
- application logic failure

Continue application investigation.

---

## Request Processed Successfully

If logs confirm successful execution:

- application may not be the failure point
- response ownership should be revisited
- downstream dependencies may require investigation

Continue tracing as needed.

---

# Core Principle

> Application logs help determine how the request was processed.

Do not assume:

- the application received the request
- the application generated the response
- application ownership exists

Use:

- synchronized timestamps
- application telemetry
- correlation identifiers
- authoritative logs

to determine how the application actually handled the request.

---

# Related Content

- Step 05 – Check Origin Infrastructure Logs
- Step 07 – Validate Response Ownership
- OWASP Application Logging Guidance
- AI Guidance – Evidence Requirements
- AI Guidance – Authoritative Sources