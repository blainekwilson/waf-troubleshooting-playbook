# Troubleshooting Checklist

Use this checklist while troubleshooting reported WAF issues.

## Step 00: Intake and Evidence Review

- [ ] Requestor identified
- [ ] Business/application impact understood
- [ ] Exact URL or endpoint collected
- [ ] Date, time, and timezone collected
- [ ] Source IP or client location collected
- [ ] Screenshots collected, if available
- [ ] HAR file collected, if available
- [ ] HTTP request/response details collected, if available
- [ ] Existing WAF event IDs or logs collected, if available
- [ ] Existing application/web server logs collected, if available
- [ ] Information source validated
- [ ] Required technical owners identified

## Step 01: Verify the client is pointing to the WAF

- [ ] DNS resolution checked
- [ ] Internal and external DNS compared
- [ ] No hosts file override identified
- [ ] No hardcoded origin IP identified
- [ ] Split DNS behavior reviewed
- [ ] Server-to-server bypass ruled out or documented
- [ ] Third-party endpoint usage reviewed
- [ ] Rogue or unmanaged API ruled out or documented

## Step 02: Verify the request reaches the WAF

- [ ] WAF access logs checked
- [ ] Timestamp aligned with requestor report
- [ ] Source IP checked
- [ ] Hostname checked
- [ ] Request path checked
- [ ] No evidence of pre-WAF block or routing issue

## Step 03: Confirm WAF handling

- [ ] WAF action confirmed
- [ ] Allow/block/challenge behavior identified
- [ ] Relevant security event reviewed
- [ ] Rule or policy match identified, if applicable
- [ ] Request ID captured, if available

## Step 04: Validate forwarding to origin

- [ ] Origin configuration reviewed
- [ ] Forwarding headers reviewed
- [ ] TLS/SNI behavior reviewed
- [ ] Load balancer target reviewed

## Step 05: Check origin logs

- [ ] Web server logs checked
- [ ] Application logs checked
- [ ] Firewall logs checked, if needed
- [ ] Load balancer logs checked, if needed

## Step 06: Compare response codes across layers

- [ ] Client response code captured
- [ ] WAF response code captured
- [ ] Load balancer response code captured
- [ ] Web server response code captured
- [ ] Application response code captured