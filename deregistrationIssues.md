# Deregistration Issues 

### Troubleshooting Steps: 

- Distinguish UE-initiated vs network-initiated 

- Check deregistration type and reason 

- Verify implicit vs explicit deregistration 

- Review follow-on actions 

### PCAP Analysis: 

##### UE-Initiated: 

- Capture Deregistration Request from UE 

- `Check Deregistration Type`: 

    - Normal de-registration 

    - Switch off (power down) 

    - Remove USIM 

- Verify 5GS deregistration type: 

    - 3GPP access 

    - Non-3GPP access 

    - Both 

- Look for Deregistration Accept from AMF 

##### Network-Initiated: 

- Look for Deregistration Request from AMF 

- `Check Deregistration Type`: 

    - Re-registration required 

    - 5GS services not allowed 

    - 3GPP access not allowed 

- `Verify 5GMM Cause`: 

    - #3: Illegal UE 

    - #5: PLMN not allowed 

    - #7: 5GS services not allowed 

    - #10: Implicitly de-registered 

- Look for Deregistration Accept from UE 

##### Implicit Deregistration: 

- Timer T3520 (deregistration timer) expiry 

- Multiple failed paging attempts 

- Network decides to remove context without explicit messaging