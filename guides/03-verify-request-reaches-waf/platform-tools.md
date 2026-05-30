## Windows: PowerShell Test-NetConnection

Verify TCP connectivity to WAF IP and port:

```powershell
Test-NetConnection -ComputerName <WAF_IP> -Port <PORT> -Verbose
```

Example:
```powershell
Test-NetConnection -ComputerName 192.0.2.10 -Port 443 -Verbose
```

Expected output shows:
- `TcpTestSucceeded : True` - TCP connection successful
- Latency information

**Limitations:**
- Only confirms TCP connectivity
- Does not verify TLS handshake
- Does not verify HTTP response
- Does not identify WAF

**Next step:** Use `curl` for full HTTP testing.

## Linux and macOS: netcat (nc)

Verify TCP connectivity using netcat:

```bash
nc -zv <WAF_IP> <PORT>
```

Example:
```bash
nc -zv 192.0.2.10 443
```

Expected output:
```
Connection to 192.0.2.10 port 443 [tcp/https] succeeded!
```

**Limitations:**
- Only confirms TCP connectivity
- Does not verify TLS handshake
- Does not verify HTTP response
- Does not identify WAF

**Next step:** Use `curl` for full HTTP testing.

## Cross-Platform: curl

Test full HTTP connection, TLS handshake, and HTTP request/response on Windows, macOS, or Linux:

```bash
curl -v https://<WAF_IP>/ -H "Host: <FQDN>"
```

Example:
```bash
curl -v https://192.0.2.10/ -H "Host: example.com"
```

The `-v` (verbose) flag displays:
- TCP connection details
- TLS certificate information
- TLS protocol and cipher negotiated
- HTTP request headers sent
- HTTP response status code
- HTTP response headers received
- Response body (if any)

### What to Look For

**TCP connection established:**
```
Connected to 192.0.2.10 (192.0.2.10)
```

**TLS handshake successful:**
```
SSL certificate verify ok
```
or certificate details showing issuer and validity dates

**HTTP response received:**
```
< HTTP/1.1 200 OK
< HTTP/1.0 403 Forbidden
```

**Response headers indicating WAF:**
```
< Server: <WAF_PRODUCT_NAME>
< X-Frame-Options: SAMEORIGIN
< X-XSS-Protection: 1; mode=block
```

**Complete example output:**

```bash
$ curl -v https://192.0.2.10/ -H "Host: example.com"
*   Trying 192.0.2.10:443...
* Connected to 192.0.2.10 (192.0.2.10) port 443 (#0)
* ALPN, offering h2
* ALPN, offering http/1.1
* successful CONNECT_TO host lock hash == e0ecd2f5
*   Verify return code: 0 (ok)
> GET / HTTP/1.1
> Host: example.com
> User-Agent: curl/7.68.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Date: Thu, 30 May 2026 10:15:32 GMT
< Content-Type: text/html
< Server: WAF-Product-Name/1.0
< X-Frame-Options: DENY
<
[response body...]
```

### Certificate Information Only

Get certificate details without making HTTP requests:

```bash
curl -I --cacert /path/to/ca.crt https://<WAF_IP>/ -H "Host: <FQDN>"
```

### Bypass Certificate Validation

**Use cautiously for testing only** - bypassing certificate validation is insecure:

```bash
curl -k -v https://<WAF_IP>/ -H "Host: <FQDN>"
```

The `-k` flag ignores certificate verification errors. This is useful for:
- Testing self-signed certificates during development
- Testing expired certificates
- Testing certificates with hostname mismatches

**Do not use in production environments without explicit approval.**

### Save Full Response to File

Capture complete response for detailed analysis:

```bash
curl -v https://<WAF_IP>/ -H "Host: <FQDN>" > response.txt 2>&1
```

This redirects both standard output and error output to a file for review.

## Public Tools: SSL Labs

**[SSL Labs SSL Test](https://www.ssllabs.com/ssltest/)**

1. Navigate to https://www.ssllabs.com/ssltest/
2. Enter your public DNS name
3. Run the scan
4. Review results:
   - **Certificate**: Verify issuer and validity dates match WAF configuration
   - **Protocols**: Shows supported TLS versions
   - **Cipher Suites**: Shows supported encryption algorithms
   - **Handshake Simulation**: Shows which clients can connect successfully

**Use for:**
- External validation from public internet
- Identifying protocol/cipher compatibility issues
- Comparing with known WAF TLS fingerprints
- Verifying certificate configuration

**Limitations:**
- Requires public DNS name
- Requires external connectivity (public IP)
- Takes time to complete scan (5-10 minutes typical)

## Public Tools: Security Headers

**[Security Headers](https://securityheaders.com/)**

1. Navigate to https://securityheaders.com/
2. Enter your public DNS name
3. Run the scan
4. Review response headers for:
   - WAF-identifying headers
   - Security headers configuration
   - Headers matching known WAF products

**Use for:**
- Identifying WAF response headers
- Validating security header configuration
- Comparing with known WAF configurations
- External verification

**Limitations:**
- Requires public DNS name
- Requires external connectivity (public IP)
- Shows only response headers (not full response)
