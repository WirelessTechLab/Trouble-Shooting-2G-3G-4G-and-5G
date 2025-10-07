# Dedicated bearer activation issues: 

### Check: 
PCRF policy, QoS mismatch. 

### Troubleshooting Steps: 

- Check PGW and PCRF connectivity (Gx interface) 

- Verify policy rules for dedicated bearer creation 

- Review QoS parameters and TFT (Traffic Flow Template) 

- Check MME, SGW, PGW resources 

- Verify UE support for multiple bearers 

- Review charging rules and policies 

- Check E-RAB establishment at eNodeB 

 

### PCAP: 
CCR/CCA (Gx), Bearer Resource Command/Failure. 

### What to Check: 

- Capture Diameter Credit-Control-Request (CCR) on Gx interface 

- Look for Credit-Control-Answer (CCA) with PCC rules 

- Check Create Bearer Request from PGW to SGW to MME 

- Verify Bearer Context with: 

- Linked EPS Bearer ID (default bearer) 

- QoS parameters (GBR, MBR) 

- TFT (packet filters) 

- Look for Bearer Resource Allocation Request (if UE-initiated) 

- Check E-RAB Setup Request for dedicated bearer 

- Verify E-RAB Setup Response from eNodeB 

##### Look for failure cause codes: 

- Radio resources not available 

- No user plane resources available 

- Semantic error in TFT 

- Check Activate Dedicated EPS Bearer Context Request to UE 

- Verify Activate Dedicated EPS Bearer Context Accept from UE 

- Look for Create Bearer Response completing the procedure 