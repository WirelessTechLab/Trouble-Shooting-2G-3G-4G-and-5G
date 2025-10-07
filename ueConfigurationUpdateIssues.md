# UE Configuration Update Issues 

### Troubleshooting Steps: 

- Check AMF-initiated configuration update command 

- Verify NSSAI updates 

- Review service area restrictions 

- Check configuration update acknowledgment 

### PCAP Analysis: 

- Capture Configuration Update Command from AMF 

- Check Configuration Update Indication: 

    - Registration requested 

    - Acknowledgement requested 

- Look for Updated parameters: 

    - Configured NSSAI 

    - Service Area List 

    - MICO mode (Mobile Initiated Connection Only) 

    - Network slicing indication 

- Verify Configuration Update Complete from UE 

- Look for Registration Request if required by update 