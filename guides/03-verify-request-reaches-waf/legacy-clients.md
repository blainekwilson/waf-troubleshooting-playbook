## When to Troubleshoot Legacy Client Issues

**Only perform these advanced checks if:**

1. Tests from the basic sections are working (curl, Test-NetConnection, or nc show successful connections)
2. AND client error messages indicate the client cannot connect to the WAF
3. OR client traffic cannot be found in WAF logs during Step 04

In these cases, the issue may be related to older client technology that doesn't support the WAF's TLS configuration.

## Non-SNI TLS Connections

Modern TLS connections use Server Name Indication (SNI) to tell the server which certificate the client wants. Some older client technology does not support SNI.

### Symptoms of Non-SNI Problems

- Client error: "Certificate name mismatch" or "Certificate verification failed"
- Client error: "Invalid certificate" or "Certificate not trusted"
- Client error: "hostname does not match certificate"
- WAF shows no access logs for the client request (connection not even reaching HTTP layer)
- Modern tools like `curl` work fine, but legacy client fails
- Certificate in error message shows default/wildcard certificate instead of application certificate

### Test for SNI Requirement

**Using OpenSSL without SNI:**

```bash
openssl s_client -connect <WAF_IP>:443 </dev/null
```

Example:
```bash
openssl s_client -connect 192.0.2.10:443 </dev/null
```

**Using OpenSSL with SNI:**

```bash
openssl s_client -connect <WAF_IP>:443 -servername <FQDN> </dev/null
```

Example:
```bash
openssl s_client -connect 192.0.2.10:443 -servername example.com </dev/null
```

### Comparing Results

Look at the certificate information in the output. Key fields to compare:

**Certificate subject (CN field):**
```
Subject: CN=example.com (WITH SNI)
Subject: CN=*.example.com (WITHOUT SNI - generic/default cert)
```

**Issuer information:**
- With SNI: May show specific organization name in certificate
- Without SNI: May show generic WAF default certificate issuer

**Subject Alternative Names (SAN):**
- With SNI: Should include your specific domain
- Without SNI: May be missing or generic

### Sample OpenSSL Output

**With SNI (correct certificate):**
```
Certificate chain
 0 s:/CN=example.com/O=Example Corp/C=US
   i:/CN=Let's Encrypt Authority X3/O=Let's Encrypt/C=US
```

**Without SNI (generic certificate):**
```
Certificate chain
 0 s:/CN=*.waf-default.local/O=WAF Product/C=US
   i:/CN=WAF Internal CA/O=WAF Product/C=US
```

### If Certificates Differ

- **The WAF requires SNI** - The server sends different certificates based on the SNI name
- **Clients that don't support SNI will see the default certificate** - Older clients may refuse to connect
- **Check client documentation** - Look for SNI support requirements
- **Upgrade considerations** - May require client upgrade or WAF configuration change

### Using SSL Labs to Check SNI

**[SSL Labs SSL Test](https://www.ssllabs.com/ssltest/)**

1. Run scan against your public DNS name
2. Check the "Protocol Details" or "Configuration" section
3. Look for notes about SNI requirement or SNI-only certificates
4. Check "Handshake Simulation" section for clients that fail with "SNI" errors
5. Clients marked with "SNI required" will not work with non-SNI clients

### Testing Non-SNI Clients

If you have access to legacy client:

1. Capture the error message - Record exact error text and error codes
2. Check client logs - Look for certificate verification errors
3. Test with curl - If curl works but client fails, suspect SNI or cipher issue
4. Compare certificates - Use openssl to compare SNI vs non-SNI certificates

## Protocol and Cipher Compatibility

WAFs may support specific TLS protocols (TLS 1.2, TLS 1.3) and cipher suites. Older clients may not support the same protocols or ciphers.

### Symptoms of Protocol/Cipher Problems

- Client error: "Protocol mismatch"
- Client error: "Protocol not supported"
- Client error: "No shared cipher suites"
- Client error: "SSL handshake failed" or "TLS handshake failed"
- WAF shows no access logs for the client request (connection fails during TLS negotiation)
- Modern tools work, but specific legacy clients fail

### Check Supported Protocols and Ciphers

**Using SSL Labs:**

1. Run [SSL Labs SSL Test](https://www.ssllabs.com/ssltest/) against your public DNS name
2. In the results, find:
   - **Protocols** section - Shows supported TLS versions (TLS 1.0, 1.1, 1.2, 1.3, etc.)
   - **Cipher Suites** section - Shows supported cipher suites for each protocol
   - **Handshake Simulation** section - Shows which client versions can connect
3. Compare with client documentation for supported versions and ciphers

### Using sslscan (Linux/macOS)

If sslscan is available (install via `apt-get install sslscan` or `brew install sslscan`):

```bash
sslscan <WAF_IP>:443
```

Example:
```bash
sslscan 192.0.2.10:443
```

Output shows:
- Supported protocol versions (TLS 1.0, TLS 1.1, TLS 1.2, TLS 1.3, etc.)
- Supported cipher suites for each protocol
- Cipher strength (Strong, Weak, Insecure)
- Weak or deprecated ciphers

**Sample output:**
```
Protocol : TLSv1.2
Cipher : ECDHE-RSA-AES256-GCM-SHA384 (256 bits) (Strong)
Cipher : ECDHE-RSA-AES128-GCM-SHA256 (128 bits) (Strong)
Cipher : DHE-RSA-AES256-GCM-SHA384 (256 bits) (Strong)
...

Protocol : TLSv1.3
Cipher : TLS_AES_256_GCM_SHA384 (256 bits) (Strong)
Cipher : TLS_AES_128_GCM_SHA256 (128 bits) (Strong)
...
```

### Using OpenSSL to Test Specific Protocols

**Test for TLS 1.2 support:**

```bash
openssl s_client -connect <WAF_IP>:443 -tls1_2 -servername <FQDN> </dev/null
```

Example:
```bash
openssl s_client -connect 192.0.2.10:443 -tls1_2 -servername example.com </dev/null
```

**Test for TLS 1.1 support (legacy):**

```bash
openssl s_client -connect <WAF_IP>:443 -tls1_1 -servername <FQDN> </dev/null
```

**Test for TLS 1.3 support (newer):**

```bash
openssl s_client -connect <WAF_IP>:443 -tls1_3 -servername <FQDN> </dev/null
```

### Interpreting Results

**Successful connection:**
```
SSL-Session:
    Protocol : TLSv1.2
    Cipher : ECDHE-RSA-AES256-GCM-SHA384
```

Connection succeeded, server supports that protocol.

**Protocol not supported:**
```
139982267854272:error:1409E0E5:SSL routines:SSL3_GET_RECORD:ssl/tls alert unknown
```

Server does not support that protocol.

### Testing Specific Ciphers

List available OpenSSL ciphers:

```bash
openssl ciphers -v
```

Test connection with specific ciphers:

```bash
openssl s_client -connect <WAF_IP>:443 -ciphers <CIPHER_NAME> </dev/null
```

Example:
```bash
openssl s_client -connect 192.0.2.10:443 -ciphers 'AES256-GCM-SHA384' </dev/null
```

## Troubleshooting Steps for Legacy Clients

### Step 1: Collect Client Information

- Exact client name and version
- Client error message (word-for-word)
- Client logs or debug output
- Client supported protocols and ciphers (from client documentation)
- When did this client last work (if it worked before)

### Step 2: Test Modern Client

Confirm that modern clients (curl, browser) work:

```bash
curl -v https://<FQDN>/ 
```

If modern clients work, the issue is client-specific, not WAF-wide.

### Step 3: Compare Capabilities

- **Client capabilities**: Check documentation for supported TLS versions and ciphers
- **WAF capabilities**: Run SSL Labs or sslscan to get WAF configuration
- **Overlap**: Find common protocols and ciphers between client and WAF

### Step 4: Test for Non-SNI

Compare certificates with and without SNI:

```bash
openssl s_client -connect <WAF_IP>:443 -servername <FQDN> </dev/null | grep "CN="
openssl s_client -connect <WAF_IP>:443 </dev/null | grep "CN="
```

If certificates differ, the issue may be SNI-related.

### Step 5: Identify Protocol/Cipher Issue

If Step 3 shows no overlap in supported protocols or ciphers:
- Client and WAF cannot negotiate a common protocol or cipher
- Connection fails during TLS handshake
- WAF shows no access logs

### Resolution Options

- **Upgrade the client** - Update to version supporting modern protocols/ciphers
- **Change WAF policy** - Enable older protocols or ciphers (consider security implications)
- **Use compatibility proxy** - Interpose a proxy that bridges old and new protocols
- **Migrate client workload** - Move to platform that supports modern TLS

## Documentation

When documenting legacy client compatibility:

- Document the exact client, version, and supported protocols/ciphers
- Document which WAF protocol/cipher settings support the client
- Document any workarounds or configuration changes made
- Note security implications of supporting older protocols
- Plan for eventual migration away from legacy clients
