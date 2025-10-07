# DNS resolution failures (APN):

### CHECK:
- DNS server reachability from GGSN/PGW. 

### Troubleshooting Steps: 
- Verify DNS server configuration on SGSN 
- Test DNS queries manually for APN FQDN 
- Check DNS server availability and response times 
- Verify APN naming format (e.g., apn.operator.com) 
- Review DNS records on authoritative servers 
- Check firewall rules blocking DNS traffic 
- Verify DNS cache and TTL settings  

### PCAP Analysis:
- Look for DNS Query/Response on port 53; check if response is missing or NXDOMAIN.

### What to Check:
- Capture DNS Query packets from SGSN 
- Look for DNS query type A or AAAA records for APN 
- Check DNS Response (should contain GGSN IP addresses) 
- Look for DNS error codes: 
- NXDOMAIN (non-existent domain) 
- SERVFAIL (server failure) 
- Query timeout 
- Verify DNS transaction ID matching 
- Check query timing (delays > 3 seconds indicate issues) 
- Look for multiple retry attempts 
- Verify resolved IP addresses match configured GGSNs 