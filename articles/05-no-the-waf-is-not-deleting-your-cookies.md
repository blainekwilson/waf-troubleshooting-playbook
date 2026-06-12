# No, the WAF Is Not Deleting Your Cookies

One of the most common statements heard by WAF teams is:

> "The application worked before the WAF was added."

Closely followed by:

> "The WAF must be deleting our cookies."

Or:

> "The WAF is removing headers required by the application."

Sometimes that is true.

Most of the time it is not.

This article covers a real-world troubleshooting investigation that initially appeared to be a WAF issue but ultimately turned out to be an application configuration problem.

More importantly, it demonstrates why evidence should drive troubleshooting—not assumptions.

---

# The Situation

An internal application was functioning correctly on the corporate network.

The application was later published to the Internet behind a WAF.

Immediately after deployment, users began reporting authentication and session-related issues.

The application team investigated and reached a conclusion:

> The WAF must be deleting cookies or HTTP headers required by the application.

At first glance, the theory sounded reasonable.

The only significant architectural change was the addition of the WAF.

Unfortunately:

reasonable is not the same thing as proven.

---

# The Problem With Assumptions

The application team had a theory.

What they did not have was evidence.

Specifically:

- no packet captures
- no server-side tracing
- no request correlation
- no proof that cookies were missing
- no proof that headers were modified

Only a plausible explanation.

This is where many troubleshooting investigations stall.

A theory becomes accepted as fact.

The investigation narrows prematurely.

Evidence collection stops.

---

# Gathering Evidence

The first step was collecting authoritative evidence.

On the client side we captured:

- HAR files
- browser requests
- browser responses
- cookies
- HTTP headers

This provided visibility into what the client was actually sending and receiving.

However, we still needed to answer an important question:

> What did the application server receive?

---

# Discovering IIS FREB

During the investigation I discovered IIS Failed Request Event Buffering (FREB).

FREB provides detailed request processing information directly from IIS.

By enabling FREB on the IIS server we were able to capture:

- incoming requests
- request headers
- cookies
- processing details
- request handling behavior

Most importantly:

FREB allowed us to compare what the client sent with what IIS actually received.

---

# Correlating Client and Server Evidence

Using:

- HAR files from the client
- FREB logs from IIS

we were able to compare requests at both ends of the transaction.

The results were clear.

The cookies were present.

The headers were present.

The WAF was forwarding them correctly.

The application server was receiving them correctly.

The evidence disproved the original theory.

The WAF was not deleting cookies.

The WAF was not removing headers.

---

# What the Evidence Told Us

At this point the investigation changed.

Instead of asking:

> "What is the WAF deleting?"

we started asking:

> "Why is authentication failing when the WAF is present?"

That is a much better troubleshooting question.

The first question assumes ownership.

The second question follows the evidence.

---

# Following the Authentication Flow

Using AI-assisted troubleshooting and the collected evidence, we reviewed the application's authentication flow.

Attention shifted toward:

- authentication configuration
- redirect behavior
- trust relationships
- OpenID Connect processing

This eventually led us to the root cause.

---

# The Real Problem

The issue was not cookie handling.

The issue was not header handling.

The issue was not the WAF.

The application's OpenID Connect configuration did not trust the WAF.

Once the trust configuration was corrected, authentication functioned normally.

The application worked as expected.

No WAF changes were required.

---

# Why This Matters

This investigation highlights a common troubleshooting pattern.

A new component is introduced.

Users experience a problem.

The new component becomes the primary suspect.

Sometimes that suspicion is correct.

Many times it is not.

Without evidence, troubleshooting becomes:

- assumption-driven
- slower
- more expensive
- more frustrating

---

# The Value of Multiple Evidence Sources

One lesson from this investigation is the importance of collecting evidence from multiple layers.

Client evidence:

- HAR files
- browser developer tools
- raw HTTP requests and responses

Server evidence:

- IIS FREB
- web server logs
- application logs

Infrastructure evidence:

- WAF logs
- proxy logs
- load balancer logs

The more layers you can correlate, the easier it becomes to identify ownership.

---

# Evidence Should Drive Ownership

When troubleshooting web applications behind a WAF:

avoid asking:

> "How is the WAF breaking the application?"

Instead ask:

> "What does the evidence show?"

That small change in mindset often determines whether an investigation takes hours or weeks.

---

# Core Principle

> Evidence should determine ownership.

Not timing.

Not assumptions.

Not reputation.

And not whichever system was deployed most recently.

In this case:

- HAR files showed what the client received
- FREB showed what IIS received
- WAF logs showed how the request was handled

Together they told a consistent story.

The WAF was not deleting cookies.

The application simply did not trust it.

---

# Related Content

- Article – Gathering Evidence Before Troubleshooting
- Article – AI-Assisted Troubleshooting Starts With Evidence
- Step 04 – Confirm WAF Handling
- Step 05 – Check Origin Infrastructure Logs
- Step 06 – Check Application Logs