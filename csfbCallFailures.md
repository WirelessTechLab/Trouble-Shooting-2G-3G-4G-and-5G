# CSFB call failures: (CSFB Call Failures to 3G/2G)

### Check:

MME–MSC interaction. 

### Troubleshooting Steps: 

- Check SGs interface connectivity between MME and MSC 

- Verify UE support for CSFB 

- Review Combined Attach procedures 

- Check 2G/3G coverage availability 

- Verify MSC configuration for CSFB 

- Review LAI (Location Area Identity) mapping 

- Check redirection vs. handover method configuration 

- Verify authentication and TMSI allocation 

 

### PCAP:
Extended Service Request → Failure cause. 

### What to Check: 

- Look for Combined Attach Request (EPS/IMSI attach) 
 
- Check SGs Location Update Request from MME to MSC 

- Verify Location Update Accept from MSC 

- Capture Extended Service Request from UE with CSFB indicator 

- Look for SGs Paging Request from MSC to MME 

- Check S1AP Paging from MME to eNodeB 

- Verify Service Request from UE 

- Look for RRC Connection Reconfiguration with: 

- Redirection info (to 2G/3G frequency), OR 

- Handover from E-UTRAN command 

- Check NAS message (CM Service Request) tunneled in RRC 
 
- For redirection method: 
 
- Verify System Information reading in target RAT 
 
- Look for RRC Connection Release with redirection 
 
- Check attach in target RAT (2G/3G) 

- Verify CM Service Request in 2G/3G 

### For handover method: 

- Check S1AP Handover Required to 2G/3G 

- Look for PS-CS Handover procedures 

- Verify Handover Command with target RAT info 

- Look for failure causes: 

- CSFB not allowed 

- Congestion 

- No cells in target RAT 

- Network failure 

- Check LAU (Location Area Update) in target network 

- Verify call establishment after successful CSFB 