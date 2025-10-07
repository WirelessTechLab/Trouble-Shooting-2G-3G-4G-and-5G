#   Attach failures (HLR/AuC): Due to Authentication Issues (HLR/AuC):

### CHECK:
- Authentication, security mode. 

### Troubleshooting Steps: 
- Check HLR/AuC connectivity from SGSN 
- Verify IMSI provisioning and authentication keys 
- Review authentication vector generation 
- Check SIM card authentication parameters 
- Verify MAP protocol operation 
- Review SS7/SIGTRAN connectivity 
- Check for authentication counter synchronization issues 
 

### PCAP Analysis:
-  Attach Request/Accept/Reject; MAP Authentication info.

### What to Check:
- Capture Attach Request from UE 
- Look for MAP Send Authentication Info from SGSN to HLR 
- Check authentication triplets/quintuplets in response: 
- RAND (random challenge) 
- SRES/XRES (expected response) 
- Kc/CK/IK (ciphering/integrity keys) 
- AUTN (authentication token for 3G) 
- Verify Authentication and Ciphering Request to UE 
- Check Authentication and Ciphering Response from UE 
- Look for attach reject with cause: 
- Authentication failure 
- MAC failure 
- Synch failure 
- Verify sequence number in AUTN 
- Check for authentication vector exhaustion   