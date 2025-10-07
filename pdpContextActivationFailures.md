# PDP context activation failures (SGSN–GGSN): 

### CHECK:
-  APN config, GTP-C signaling, authentication. 

### Troubleshooting Steps:
- Check SGSN and GGSN logs for error messages 
- Verify GTP-C tunnel establishment 
- Check APN configuration on GGSN 
- Verify subscriber profile and PDP context allowance in HLR 
- Check IP address pool availability on GGSN 
- Review Gn/Gp interface connectivity 
- Verify authentication and charging interfaces 

### PCAP Analysis:
- On Gn interface, verify Create PDP Context Request/Response; check cause code.

### What to Check:
- Capture Create PDP Context Request from SGSN to GGSN 
- Check Create PDP Context Response (should have cause code 128 = - success) 
- Look for failure cause codes: 
- No resources available 
- APN access denied 
- Missing or unknown APN 
- User authentication failed 
- Verify APN name in request matches GGSN configuration 
- Check QoS parameters negotiation 
- Verify GTP-C TEID (Tunnel Endpoint Identifier) assignment 
- Look for Update PDP Context messages if modification occurs 
- Check Delete PDP Context for premature session termination 