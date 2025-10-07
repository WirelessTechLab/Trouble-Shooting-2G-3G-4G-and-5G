# Service Request Failures (Transition from IDLE to CONNECTED) 

### Troubleshooting Steps: 

- Check paging response 

- Verify NAS security context 

- Review RRC connection establishment 

- Check initial context setup at AMF/gNB 

- Verify PDU session activation 

### PCAP Analysis: 

- `Look for Paging message from AMF`: 

    - UE Identity: 5G-S-TMSI 

    - TAI List: Paging areas 

    - Paging DRX: Cycle for paging 

    - Paging Priority: For different services 

- `Capture Service Request from UE`: 

    - `Service Type`: 

        - Signaling 

        - Data 

        - Mobile Terminated services 

        - Emergency services 

        - Emergency services fallback 

    - ngKSI: Security context 

    - 5G-S-TMSI: Temporary identity 

    - Uplink Data Status: PDU sessions with data 

    - PDU Session Status: Active sessions 

- Check Service Accept from AMF 

- `Or Service Reject with causes`: 

    - #9: UE identity cannot be derived 

    - #10: Implicitly de-registered 

    - #28: Temporarily unavailable 

- `Verify Initial Context Setup Request (AMF → gNB)`: 

    - Allowed NSSAI 

    - UE Security Capabilities 

    - Security Key 

    - PDU Session Resource Setup Request List 

- Look for Initial Context Setup Response from gNB 

- Check PDU Session Resource Setup for active sessions 