# SRVCC Drop to 3G: 

### Check: 
IMS → MSC handover signaling. 

### Troubleshooting Steps: 

- Check SRVCC support in MME, MSC, IMS 
 
- Verify E-UTRAN to UTRAN handover procedures 

- Review SRVCC configurations and parameters 

- Check IMS session transfer procedures (STN-SR) 

- Verify MSC anchoring and call continuation 

- Review codec negotiation during SRVCC 

- Check bearer splitting (PS/CS) procedures 

- Test in different radio conditions 

- Verify target 3G cell availability and capacity 


### PCAP: 
SIP INVITE re-INVITE/Bye; SRVCC Handover Required/Failure. 

### What to Check: 

##### Pre-SRVCC Phase: 

- Verify VoLTE call active (SIP session established) 

- Check IMS dedicated bearer (QCI 1) active 

- Look for Measurement Reports indicating weak LTE signal 

- Verify SRVCC capability in UE and network 

##### SRVCC Execution Phase: 

- Look for S1AP Handover Required with SRVCC indication 

- Check PS to CS Request from MME to MSC (Sv interface) 

- Verify MSC allocates CS resources for call continuation 

- Look for SIP INVITE from MSC to IMS (for session transfer) 

- Check STN-SR (Session Transfer Number) usage 

- Verify PS to CS Response from MSC to MME 

- Look for Handover Command to UE with target 3G cell info 

- Check RANAP Relocation Request to target RNC 

- Verify Relocation Request Acknowledge from RNC 

##### Target Network Phase: 

- Look for Handover Complete in target 3G cell 

- Check CS call establishment in UMTS 

- Verify Assignment Complete for CS bearer 

- Look for SIP BYE to release IMS leg 

- Check bearer release in LTE (default and dedicated) 

##### Failure Scenarios - Check for: 

##### PS to CS Request rejection with causes: 

    - SRVCC not allowed 

    - MSC resource unavailable 

    - Target cell not available 


- Handover Preparation Failure at target RNC 
 
- Missing STN-SR in configuration 

- IMS session transfer failure (SIP errors) 

- CS bearer allocation failure in target 

- RRC Connection Re-establishment (indicates HO failure) 

##### Call drop without proper session transfer: 

    - Look for Release messages in both LTE and UMTS 

    - Check cause codes: radio link failure, handover failure 

- Codec mismatch between IMS (EVS/AMR-WB) and CS (AMR-NB) 

- Late handover (UE already lost LTE signal) 

- Dual Radio issues (some UEs don't support simultaneous PS/CS) 

##### Post-Failure Analysis: 

- Check if call continues in LTE (SRVCC abandoned) 

- Look for fallback to CSFB if SRVCC fails 

- Verify IMS re-registration if call dropped completely 

- Check E-RAB release causes for IMS bearer 

- Look for abnormal release procedures 