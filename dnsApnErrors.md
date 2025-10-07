# DNS/APN errors: (DNS/APN Configuration Errors) 

### Check: 
PGW DNS config. 

### Troubleshooting Steps: 

- Verify APN configuration in HSS subscriber profile 

- Check APN-FQDN to PGW IP resolution 

- Test DNS queries from MME/SGW 

- Verify DNS server configuration and availability 

- Check APN naming conventions 

- Review PGW selection algorithm 

- Verify APN access restrictions 

### PCAP: 
DNS Query/Response failure. 

### What to Check: 

- Look for APN name in Attach Request or PDN Connectivity Request 

- Check DNS A/AAAA query from MME/SGW for APN-FQDN 

- Verify DNS response with PGW IP addresses 

##### Look for DNS error codes: 

- NXDOMAIN (domain doesn't exist) 

- SERVFAIL (DNS server failure) 

- No response (timeout) 

- Check APN-OI Replacement in subscriber profile 

- Verify APN restriction field in Create Session messages 

- Look for context request rejection due to APN not subscribed 

- Check multiple APN configurations in HSS 

- Verify APN-AMBR (Aggregate Maximum Bit Rate) values 

- Look for PGW selection based on DNS results 