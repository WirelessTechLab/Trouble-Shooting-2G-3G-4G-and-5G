# Default bearer setup failures: 

### Check: 
PGW connectivity, APN config. 

### Troubleshooting Steps: 

- Check MME, SGW, and PGW logs 

- Verify S11 and S5/S8 interface connectivity 

- Check APN configuration on PGW 

- Verify IP address pool availability 

- Review QoS profile matching 

- Check GTP-C tunnel establishment 

- Verify DNS configuration for APN 

### PCAP: 
Check Create Session Request/Response (S11). 

### - What to Check: 

- Look for Create Session Request from MME to SGW (S11) 

- Check Create Session Request from SGW to PGW (S5/S8) 

- Verify Create Session Response from PGW to SGW 

- Check Create Session Response from SGW to MME 

- Look for GTP-C cause codes in responses: 

- 64: No resources available 

- 65: All dynamic addresses are occupied 

- 193: APN access denied 

- 211: Request rejected 

- Verify APN name in request 

- Check Bearer Context IE with: 

- EPS Bearer ID 

- Bearer QoS 

- GTP-U TEIDs (uplink/downlink) 

- Look for PDN type (IPv4, IPv6, IPv4v6) 

- Verify PGW address allocation 

- Check E-RAB Setup Request from MME to eNodeB 

- Look for E-RAB Setup Response (success or failure) 