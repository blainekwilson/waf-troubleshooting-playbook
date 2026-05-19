## Using nslookup

Run:

nslookup example.com

Verify:
- Returned IP matches WAF IP range
- No unexpected internal IPs

## Using dig

dig example.com +short

## Using ping

ping example.com

Note: ICMP may be blocked by some WAFs

## Common pitfalls

- Local DNS cache
- Split-horizon DNS
- VPN altering resolution