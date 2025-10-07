# VoLTE registration failures: (IMS Attach Issues) 

### Check: 
IMS reachability, SIP over Diameter. 

### Troubleshooting Steps: 

- Check IMS subscription in HSS 

- Verify P-CSCF discovery (via PCO or DNS) 

- Review SIP REGISTER procedures 

- Check IPSec tunnel establishment (if used) 

- Verify authentication (IMS AKA) 

- Review S-CSCF assignment 

- Check dedicated bearer for IMS signaling 

 
### PCAP: 
SIP REGISTER → 200 OK; missing response or 4xx/5xx errors. 

### What to Check: 

- Look for PCO (Protocol Configuration Options) in Attach Accept: 

- P-CSCF IPv4/IPv6 address 

- Check DNS query for P-CSCF discovery (if PCO not used) 

- Capture SIP REGISTER request from UE to P-CSCF 

- Verify 401 Unauthorized response with challenge 

- Check SIP REGISTER with authentication credentials 

- Look for 200 OK response confirming registration 

- Verify IMS private/public identities (IMPI/IMPU) 

- Check IPSec ESP packets (if security association established) 

- Look for dedicated bearer creation for IMS signaling (QCI 5) 

- Verify Diameter Multimedia-Auth-Request/Answer (Cx interface) 

- Check S-CSCF assignment 

- Look for SIP error responses: 

- 403 Forbidden (not authorized) 

- 404 Not Found (user not found) 

- 500 Server Error 