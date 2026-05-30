## Verification Approach

To verify that HTTP requests reach the WAF, test the complete connection flow:

1. **TCP connection** - Establish a TCP connection to the WAF IP and port
2. **TLS handshake** - Negotiate encryption using TLS protocol
3. **HTTP request** - Send HTTP request over the encrypted connection
4. **HTTP response** - Receive HTTP response from the WAF
5. **Response validation** - Examine response for WAF indicators

## TCP Connections and TLS Handshakes

When a client connects to the WAF:

1. **TCP three-way handshake** - Client and WAF establish a TCP connection using SYN, SYN-ACK, ACK packets
2. **TLS handshake** - Client and WAF negotiate encryption using TLS protocol (typically TLS 1.2 or 1.3)
3. **HTTP request** - Client sends HTTP request over the established encrypted connection
4. **HTTP response** - WAF responds with HTTP status code and headers

All of these steps must complete successfully for a request to "reach the WAF" and be processed.

Tools verify this by:
- Establishing a TCP connection to the WAF IP and port
- Completing the TLS handshake to verify the connection is encrypted
- Sending an HTTP request and capturing the response
- Examining response headers and body for WAF indicators

## Why ICMP and Ping Are Not Evidence

**Ping (ICMP) does not prove TCP connections work.**

- Ping uses ICMP protocol, not TCP
- A WAF can respond to ICMP while blocking TCP traffic
- A WAF can drop ICMP packets while accepting TCP connections
- Many firewalls and WAFs are configured to ignore ICMP

**Ping evidence is not sufficient to prove requests are reaching the WAF.**

Instead, verify the actual TCP connection and HTTP request/response flow.

## Expected Response Indicators

Strong indicators that responses come from the WAF:

- HTTP response headers contain WAF-identifying headers (e.g., WAF product name in `Server` header, WAF-specific cookies)
- Response status codes match WAF behavior patterns (e.g., 403 Forbidden with WAF error page)
- Response body contains WAF block page or WAF error messages
- TLS certificate matches WAF's certificate (not origin server's)
- Response timing matches WAF characteristics (not origin server delays)

## Tools Overview

| Tool | Platform | Purpose | Limitations |
|---|---|---|---|
| `Test-NetConnection` | Windows PowerShell | TCP connectivity test | No HTTP response, no TLS details |
| `nc` (netcat) | Linux/macOS | TCP connectivity test | No HTTP response, no TLS details |
| `curl` | Windows/Linux/macOS | Full HTTP+TLS test | Requires tool installation |
| `openssl` | Linux/macOS | TLS handshake and certificate inspection | Complex command-line options |
| SSL Labs | Web-based | External TLS validation | Public scan, external IP required |
| Security Headers | Web-based | Response header analysis | Public scan, external IP required |

## When to Use Each Tool

**Quick TCP test:**
- Use `Test-NetConnection` on Windows or `nc` on Linux/macOS
- Confirms port is open and reachable
- Does NOT verify HTTP response or WAF processing

**Full HTTP+TLS verification:**
- Use `curl` on any platform
- Verifies complete connection flow
- Best for initial troubleshooting

**Certificate inspection:**
- Use `openssl` for TLS handshake details
- Use SSL Labs for external validation
- Useful when certificate mismatch is suspected

**Response header analysis:**
- Use `curl -v` to see all response headers
- Use Security Headers web tool for external validation
- Useful when identifying WAF-specific headers
