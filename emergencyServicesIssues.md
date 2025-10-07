# Emergency Services Issues 

### Troubleshooting Steps: 

- Check emergency registration without credentials 

- Verify emergency PDU session with DNN="sos" or similar 

- Review LCS (Location Services) for emergency location 

- Check E-CSCF (Emergency CSCF) configuration 

- Verify LRF (Location Retrieval Function) and ESRP routing 

- Review callback number configuration 

PCAP Analysis: 

- Look for Registration Request with: 

    - Registration type: Emergency registration 

    - Follow-on request indicator 

- Check Registration Accept without full authentication 

- Verify Emergency PDU Session Establishment Request: 

    - DNN: "sos" or operator-specific emergency DNN 

    - PDU session type: IPv4, IPv6, or IPv4v6 

- Look for Emergency indicator in session setup 

- Check LCS procedures for location: 

    - LMF (Location Management Function) query 

    - NRPPa (positioning protocol) 

    - Location estimate in NGAP 

- Verify SIP INVITE to emergency number: 

    - Request-URI: urn:service:sos or specific emergency number 

    - Geolocation header: Location information 

    - P-Asserted-Identity: Callback number 

- Look for E-CSCF involvement in routing 

- Check ESRP (Emergency Services Routing Proxy) selection of PSAP 