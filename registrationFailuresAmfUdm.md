# Registration Failures (UE to AMF / UDM) 

### Troubleshooting Steps: 

##### 1. Check AMF-UDM Connectivity (Nudm Interface) 

- Verify HTTP/2 connectivity between AMF and UDM 

- Check network reachability (ping, traceroute) 

- Review NRF (NF Repository Function) service discovery 

- Verify TLS certificates if security enabled 

- Check firewall rules and routing 

##### 2. Verify UE Provisioning in UDM 

- Confirm SUPI (Subscription Permanent Identifier) exists in UDM 

- Check subscription profile completeness 

- Verify allowed NSSAI (Network Slice Selection Assistance Information) 

- Confirm DNN (Data Network Name) subscriptions 

- Check UE's access restrictions and roaming permissions 

- Verify SUCI (Subscription Concealed Identifier) to SUPI mapping 

##### 3. Check AUSF Authentication Procedures 

- Verify AUSF connectivity with UDM (Nausf interface) 

- Check authentication method configuration (5G-AKA or EAP-AKA') 

- Review authentication vector generation (RAND, AUTN, XRES*, KAUSF) 

- Verify USIM card authentication parameters 

- Check for sequence number synchronization issues 

- Review authentication counter (SQN) in UDM 

##### 4. Review AMF Capacity and Performance 

- Check AMF CPU and memory utilization 

- Monitor concurrent registrations vs. capacity 

- Review AMF load balancing configuration 

- Check for AMF overload conditions 

- Verify AMF set and region configurations 

- Review timer configurations (T3510, T3520, T3550) 

##### 5. Verify gNB ↔ AMF NGAP Signaling 

- Check SCTP associations between gNB and AMF

- Verify NG Setup procedures completed successfully 

- Review GUAMI (Globally Unique AMF Identifier) configuration 

- Check TAC (Tracking Area Code) mapping 

- Verify gNB sends correct PLMN and cell identity 

- Monitor for NGAP error indications 

##### 6. Check Allowed NSSAI (Slice Selection) 

- Verify requested S-NSSAI is subscribed in UDM 

- Check NSSF (Network Slice Selection Function) policies 

- Review slice availability in AMF 

- Confirm network slice instance configuration 

- Check for slice admission control policies 

- Verify mapping between requested and allowed NSSAI 

##### 7. Review Security Context 

- Check NAS security mode command completion 

- Verify integrity protection algorithms (NIA1, NIA2, NIA3) 

- Check ciphering algorithms (NEA0, NEA1, NEA2, NEA3) 

- Review KAMF derivation and distribution 

##### 8. Check Registration Type 

- Distinguish between Initial, Mobility, Periodic registration 

- Verify appropriate procedure for each type 

- Check 5GMM state machines (REGISTERED, DEREGISTERED) 

##### PCAP Analysis - What to Check: 

##### N1/N2 Interface (UE ↔ gNB ↔ AMF): 

##### 1. Capture Registration Request (NAS over NGAP) 

- Look for InitialUEMessage from gNB to AMF containing Registration Request 

- Verify 5GS registration type: Initial / Mobility / Periodic / Emergency 

- Check ngKSI (NAS key set identifier) 

- Verify 5GS mobile identity: SUCI (concealed) or 5G-GUTI 

- Check requested NSSAI (S-NSSAI: SST + SD) 

- Verify UE security capability (encryption and integrity algorithms) 

- Look for 5GMM capability IE 

- Check Last visited registered TAI 

##### 2.  Authentication Request from AMF → UE 

- Look for DL NAS Transport containing Authentication Request 

- Verify ngKSI value 

- Check RAND (random challenge) - 128 bits 

- Verify AUTN (authentication token) - 128 bits 

- Check EAP-AKA' message if EAP method used 

- Look for ABBA (Anti-Bidding down Between Architectures) parameter 

##### 3. Authentication Response from UE 

- Capture UL NAS Transport with Authentication Response 

- Verify RES* (authentication response) value 

- Check timing between request and response (should be < 2 seconds) 

- Look for Authentication Failure messages with causes: 

    - MAC failure (#20) 

    - Synch failure (#21) 

    - Security mode rejected (#24) 

##### 4. Security Mode Command/Complete 

- Look for Security Mode Command from AMF 

- Check selected NAS security algorithms: 

    - Type of integrity protection (NIA1/NIA2/NIA3) 

    - Type of ciphering (NEA0/NEA1/NEA2/NEA3) 

- Verify replayed UE security capabilities 

- Check Security Mode Complete from UE 

- Look for IMEISV (International Mobile Equipment Identity) in complete message 

##### 5. Nudm_UEAuthentication (AMF ↔ AUSF ↔ UDM) - SBI HTTP/2: 

- Capture POST request to /nudm-ueau/v1/supi-{supi}/auth-events 

- Look for Nausf_UEAuthentication_Authenticate Request from AMF to AUSF 

- Check request body with: 

    - supiOrSuci field 

    - servingNetworkName (PLMN ID) 

    - resynchronizationInfo (if synch failure) 

- Verify 201 Created or 200 OK response 

- Check response containing: 

    - authType: 5G_AKA or EAP_AKA_PRIME 

    - 5gAuthData with RAND, AUTN, HXRES* 

    - _links with callback URI 

- Look for Nudm_UEAuthentication_Get Request from AUSF to UDM 

- Verify authenticationVector in response 

##### 6. Registration Accept/Reject Messages: For Registration Reject: 

- Look for DownlinkNASTransport with Registration Accept 

- Check 5G-GUTI (new identity assigned) 

- Verify allowed NSSAI (subscribed slices) 

- Check TAI list (tracking areas) 

- Look for PDU Session Status IE 

- Verify 5GS network feature support 

- Check T3512 (periodic registration timer) value 

- Check T3502 (registration retry timer) 

##### - Verify 5GMM cause code: 

    - #3: Illegal UE (not provisioned) 

    - #5: PLMN not allowed 

    - #6: Illegal ME 

    - #7: 5GS services not allowed 

    - #8: UE identity cannot be derived 

    - #9: Implicitly de-registered 

    - #10: UE not allowed 

    - #11: PLMN not allowed 

    - #12: Tracking area not allowed 

    - #15: No suitable cells in tracking area 

    - #20: MAC failure 

    - #21: Synch failure 

    - #22: Congestion 

    - #31: Redirection to EPC required 

    - #72: Non-3GPP access to 5GCN not allowed 

- Check T3346 value (re-attempt timer for congestion) 

##### 7. Service-Based Interface (SBI) HTTP/2 Checks: 

###### a. Verify HTTP/2 status codes: 

- 200 OK: Request successful 

- 201 Created: Resource created successfully 

- 204 No Content: Successful with no body 

- 400 Bad Request: Invalid request syntax 

- 401 Unauthorized: Authentication required 

- 403 Forbidden: Not authorized for resource 

- 404 Not Found: Resource doesn't exist 

- 409 Conflict: Request conflicts with current state 

- 500 Internal Server Error: Server error 

- 503 Service Unavailable: NF temporarily unavailable 

###### b. Check JSON payload in request/response bodies 

###### c. Verify 3GPP-Sbi-Message-Priority header for priority handling 

###### d. Look for OAuth 2.0 tokens if NRF security enabled 

##### 8. NGAP Messages to Monitor: 

- InitialContextSetupRequest/Response: After registration accept 

- UEContextReleaseCommand/Complete: If registration fails 

- ErrorIndication: Network errors 

- Overload Start/Stop: AMF overload conditions 

- Paging: For idle mode UE 

- NGReset: NGAP interface reset 

##### 9. Registration Complete from UE: 

- Look for UplinkNASTransport with Registration Complete 

- Indicates successful registration procedure 

##### 10. Additional SBI Interface Traces: 

###### a. Nudm_SubscriberDataManagement (AMF to UDM): 

- GET /nudm-sdm/v2/{supi}/am-data 

- Retrieves access and mobility subscription data 

- Check nssai, subscribedUeAmbr in response 

###### b. Nudm_UECM (UE Context Management): 

- PUT /nudm-uecm/v1/{ueId}/registrations/amf-3gpp-access 

- AMF registers itself as serving AMF 

###### c. Nnrf_NFDiscovery (NRF service discovery): 

- GET /nnrf-disc/v1/nf-instances 

- Query parameters: target-nf-type, requester-nf-type 

##### Common Root Causes: 

- SUPI not provisioned in UDM 

- Authentication vector mismatch (wrong Ki/OPc) 

- Sequence number out of sync 

- Requested NSSAI not subscribed 

- AMF overload or capacity exhausted 

- NGAP signaling failures 

- Incorrect PLMN configuration 

- Security algorithm mismatch 

- UDM/AUSF connectivity issues 

- Certificate validation failures (TLS) 