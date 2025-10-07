#     Attach failures (MME–HSS):

### CHECK:
- Authentication vector mismatch, subscription profile.

### Troubleshooting Steps: 
- Check MME and HSS connectivity (S6a interface) 
- Verify Diameter protocol operation  
- Check subscriber provisioning in HSS 
- Review authentication procedures (EPS-AKA) 
- Verify IMSI in HSS database 
- Check MME capacity and performance 
- Review attach reject cause codes 
 

### PCAP Analysis:
-   NAS Attach Request → Attach Reject with cause (e.g., “EPS services not allowed”).

### What to Check:
- Capture Attach Request from UE (NAS message) 
- Look for Diameter Authentication Information Request (AIR) from MME - to HSS 
- Check Authentication Information Answer (AIA) with authentication - vectors: 
- RAND 
- XRES 
- AUTN 
- KASME 
- Verify Authentication Request sent to UE 
- Check Authentication Response from UE 
- Look for Diameter Update Location Request (ULR) to HSS 
- Check Update Location Answer (ULA) with subscriber profile 
- Look for attach reject with EMM causes: 
- #2: IMSI unknown in HSS 
- #3: Illegal UE 
- #6: Illegal ME 
- #7: EPS services not allowed 
- #8: EPS and non-EPS services not allowed 
- #20: MAC failure 
- #21: Synch failure 
- Verify Diameter result codes (2001 = success) 
- Check for S6a interface timeout issues 