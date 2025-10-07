# Network Slice Selection Issues 

### Troubleshooting Steps: 

- Check NSSAI configuration in UDM subscription 

- Verify NSSF (Network Slice Selection Function) policies 

- Review S-NSSAI availability in registration area 

- Check AMF slice support capabilities 

- Verify slice admission control 

- Review NSI (Network Slice Instance) configurations 

### PCAP Analysis: 

- Look for Requested NSSAI in Registration Request 

- Check Allowed NSSAI in Registration Accept 

- Verify Configured NSSAI from UDM subscription data 

- Look for Rejected NSSAI with causes: 

    - Slice not available in PLMN 

    - Slice not available in registration area 

    - Network slice specific authentication failed 

- Check Nnssf_NSSelection_Get request/response for slice selection 

- Verify S-NSSAI (SST + SD) in all session-related messages 

- Look for slice-specific AMF selection via NSSF