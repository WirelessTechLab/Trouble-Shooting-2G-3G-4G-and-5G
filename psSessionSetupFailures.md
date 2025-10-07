#   PS session setup failures:  (SGSN–GGSN):

### CHECK:
- SGSN–GGSN GTP-C signaling. 

### Troubleshooting Steps: 
- Check SGSN and GGSN logs for session failures 
- Verify GTP-C tunnel establishment on Gn interface 
- Check APN configuration and routing 
- Verify subscriber PDP context allowance in HLR 
- Review IP address pool availability 
- Check QoS profile matching 
- Verify GGSN selection algorithm 
 

### PCAP Analysis:
-  Verify Create PDP Context Request/Response; check rejection cause.

### What to Check:
- Capture Activate PDP Context Request from UE to SGSN 
- Look for RANAP RAB Assignment Request for PS bearer 
- Check Create PDP Context Request from SGSN to GGSN (GTP-C) 
- Verify Create PDP Context Response with cause code 
- Look for failure cause codes: 
- No resources available (199) 
- APN access denied (201) 
- Request rejected (211) 
- Check APN name in request 
- Verify NSAPI (Network Service Access Point Identifier) 
- Look for QoS profile negotiation 
- Check PDP address allocation 
- Verify GTP-U tunnel establishment  