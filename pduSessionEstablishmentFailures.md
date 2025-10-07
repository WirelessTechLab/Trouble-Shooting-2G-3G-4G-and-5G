# PDU Session Establishment Failures (SMF/UPF / DN Connection) 

### Troubleshooting Steps: 

##### 1. Check NGAP Session Setup at AMF 

- Verify AMF receives PDU Session Establishment Request from UE 

- Check AMF selection of appropriate SMF based on DNN and S-NSSAI 

- Review SMF selection function (using NRF discovery) 

- Verify AMF capacity for PDU session management 

- Check N1/N2 message handling 

##### 2. Verify N11 Interface (AMF ↔ SMF) Communication 

- Check HTTP/2 connectivity between AMF and SMF 

- Verify SMF service registration in NRF 

- Test network reachability between AMF and SMF 

- Check TLS certificate validation if enabled 

- Review OAuth token exchange 

- Monitor for HTTP errors (4xx, 5xx) 

##### 3. Check N4 Interface (SMF ↔ UPF) 

- Verify PFCP (Packet Forwarding Control Protocol) association 

- Check SMF to UPF heartbeat messages 

- Review PFCP session establishment procedures 

- Verify PDR (Packet Detection Rules) and FAR (Forwarding Action Rules) creation 

- Check QER (QoS Enforcement Rules) and URR (Usage Reporting Rules) 

- Monitor PFCP response codes 

##### 4. Validate DNN/APN Configuration 

- Check DNN name matches between UE request, subscription, and SMF config 

- Verify DNN to Data Network mapping in SMF 

- Check if DNN is configured on UPF 

- Review DNN selection rules in SMF 

- Verify wildcard DNN handling if applicable 

- Check DNN access restrictions in UDM 

##### 5. Verify IP Pool Availability at UPF 

- Check IP address pool configuration (IPv4/IPv6/IPv4v6) 

- Verify pool utilization and available addresses 

- Check for IP address exhaustion 

- Review DHCP server configuration (if used) 

- Verify NAT configuration for private IPs 

- Check IPv6 prefix delegation settings 

##### 6. Check QoS/Slice Parameters 

- Verify S-NSSAI (SST + SD) matches subscription 

- Check DNN and S-NSSAI combination is allowed 

- Review 5QI (5G QoS Identifier) values 

- Verify GBR (Guaranteed Bit Rate) resources if applicable 

- Check session-AMBR (Aggregate Maximum Bit Rate) 

- Review priority levels and ARP (Allocation Retention Priority) 

##### 7. Verify DNS Resolution for DNN 

- Test DNS query for DNN FQDN to SMF address 

- Check DNS server configuration in AMF 

- Verify DNS records exist for DNN 

- Review DNS response times 

- Check for DNS caching issues 

##### 8. Check PCF Involvement (N7 Interface) 

- Verify SMF to PCF connectivity for policy control 

- Check PCC (Policy and Charging Control) rules 

- Review session policies and QoS decisions 

- Verify charging method (online/offline) 

##### 9. Review UPF Selection 

- Check UPF selection logic in SMF 

- Verify UPF supports required features 

- Check UPF capacity and load 

- Review UPF pool configuration 

##### 10. Check User Plane Path 

- Verify N3 interface (gNB ↔ UPF) connectivity 

- Check N6 interface (UPF ↔ Data Network) routing 

- Test end-to-end connectivity through UPF 

- Review firewall rules and NAT 

###### PCAP Analysis - What to Check: 

###### NAS/NGAP Messages (N1/N2): 

##### 1. PDU Session Establishment Request from UE 

- Look for UplinkNASTransport containing PDU Session Establishment Request 

- Verify PDU session ID (1-15) 

- Check Procedure Transaction ID (PTI) 

- Verify PDU session type: IPv4, IPv6, IPv4v6, Ethernet, Unstructured 

- Check SSC mode (Session and Service Continuity): 1, 2, or 3 

- Verify requested DNN (Data Network Name) 

- Check S-NSSAI (Single Network Slice Selection Assistance Info) 

- Look for 5GSM capability IE 

- Check PCO (Protocol Configuration Options) if present 

- Verify Maximum data rate if specified 

##### 2. Nsmf_PDUSession_CreateSMContext Request (AMF → SMF) - SBI: 

a. Capture POST to /nsmf-pdusession/v1/sm-contexts 

b. Check JSON payload with: 

- supi (Subscriber Permanent Identifier) 

- pei (Permanent Equipment Identifier) 

- pduSessionId 

- dnn (Data Network Name) 

- sNssai (SST and SD) 

- servingNetwork (PLMN) 

- requestType: INITIAL_REQUEST, EXISTING_PDU_SESSION, etc. 

- n1SmMsg (Base64 encoded NAS message) 

- anType: 3GPP_ACCESS or NON_3GPP_ACCESS 

- ratType: NR, EUTRA-NR 

- ueLocation (TAI, cell ID) 

- ueTimeZone 

- Verify HTTP/2 headers (content-type: application/json) 

##### 3. - Nsmf_PDUSession_CreateSMContext Response (SMF → AMF): 

a. Look for 201 Created response 

b. Check Location header with SM Context reference 

c. Verify response body containing: 

- smContextStatusUri (callback for status updates) 

- pduSessionId 

- sNssai 

- allocatedEbiList (for interworking) 

- n2SmInfo (NGAP info for gNB) 

- n1SmMsg (NAS message for UE) 

d. Look for error responses: 

- 403 Forbidden: DNN not allowed 

- 404 Not Found: SMF context not found 

- 500 Internal Server Error: SMF processing failure 

- 503 Service Unavailable: SMF overload 

##### 4. N4 Session Establishment Request (SMF → UPF) - PFCP: 

a. Capture PFCP Session Establishment Request 

b. Verify F-SEID (Fully Qualified Session Endpoint ID) 

c. Check Create PDR (Packet Detection Rule): 

- PDR ID 

- Precedence (rule priority) 

- PDI (Packet Detection Information): 

    -   Source/destination IP 

    -   Protocol 

    -   Ports 

    -   UE IP address 

- Outer Header Removal (for GTP-U decapsulation) 

- FAR ID (linked Forwarding Action Rule) 

d. Check Create FAR (Forwarding Action Rule): 

- FAR ID 

- Apply Action: FORW, DROP, BUFF, NOCP, DUPL 

- Forwarding Parameters: 

    - Destination interface: ACCESS, CORE, SGi-LAN 

    - Network instance (DNN) 

    - Outer header creation (GTP-U encapsulation) 

    - GTP-U TEID (Tunnel Endpoint Identifier) 

e. Check Create QER (QoS Enforcement Rule): 

- QER ID 

- QFI (QoS Flow Identifier) 

- Gate Status: OPEN, CLOSED 

- MBR (Maximum Bit Rate): uplink/downlink 

- GBR (Guaranteed Bit Rate) if applicable 

f. Check Create URR (Usage Reporting Rule): 

- URR ID 

- Measurement Method: VOLUME, DURATION, EVENT 

- Reporting Triggers 

- Volume Threshold 

g. Verify Node ID of SMF 

##### 5. N4 Session Establishment Response (UPF → SMF): 

a. Look for PFCP Session Establishment Response 

b. Check Cause value: Request accepted (1) or error 

c. Verify F-SEID from UPF 

d. Check Created PDR IE with: 

- UE IP address allocated 

- F-TEID (for N3 interface - UPF side) 

e. Look for Load Control Information if UPF overloaded 

f. Check Overload Control Information 

##### 6. PDU Session Resource Setup Request (AMF → gNB) - NGAP: 

a. Capture PDUSessionResourceSetupRequest 

b. Check PDU Session Resource Setup Request Transfer IE: 

- PDU Session Aggregate Maximum Bit Rate (Session-AMBR) 

- UL NG-U UP TNL Information (UPF TEID for uplink) 

- Data Forwarding Not Possible (if applicable) 

- PDU Session Type: IPv4, IPv6, IPv4v6, Ethernet 

- S-NSSAI

- QoS Flow Setup Request List: 

    - QoS Flow Identifier (QFI) 

    - QoS Flow Level QoS Parameters: 

        - 5QI (e.g., 9 for default internet) 

        - ARP (Allocation Retention Priority) 

        - GBR QoS Flow Information (if GBR) 

    - E-RAB ID (for interworking) 

c. Verify NAS-PDU containing PDU Session Establishment Accept 

##### 7. PDU Session Resource Setup Response (gNB → AMF): 

a. Look for PDUSessionResourceSetupResponse 

b. Check PDU Session Resource Setup Response Transfer: 

- DL NG-U UP TNL Information (gNB TEID for downlink) 

- QoS Flow Setup Response List with accepted QFIs 

c. Look for PDU Session Resource Failed to Setup List if failure: 

- Check Cause values: 

    - Radio resources not available 

    - Unknown PDU Session ID 

    - Release due to NG-RAN generated reason 

    - Multiple PDU Session ID instances 

d. Verify GTP-U TEIDs (uplink from UPF side, downlink from gNB side) 

##### 8. N4 Session Modification Request (SMF → UPF): 

a. Capture after gNB response with DL TEID 

b. Look for Update FAR with: 

- gNB TEID for downlink traffic 

- Apply Action: FORW 

c. Verify PDR/FAR correlation 

##### 9. PDU Session Establishment Accept to UE: 

a. Look for DownlinkNASTransport with PDU Session Establishment Accept 

b. Check PDU session type assigned 

c. Verify SSC mode selected 

d. Check QoS rules: 

- QoS Rule ID 

- Rule precedence 

- QFI 

- Packet filter list (for QoS flow mapping) 

e. Verify QoS flow descriptions: 

- QFI 

- 5QI 

f. Check Session-AMBR values 

g. Look for PDU address (UE IP address) 

h. Check DNN if provided 

i. Verify S-NSSAI if provided 

##### 10. PDU Session Establishment Reject (if failure): 

a. Look for DownlinkNASTransport with PDU Session Establishment Reject 

b. Check 5GSM cause codes: 

- #8: Operator determined barring 

- #26: Insufficient resources 

- #27: Missing or unknown DNN 

- #28: Unknown PDU session type 

- #29: User authentication or authorization failed 

- #31: Request rejected, unspecified 

- #32: Service option not supported 

- #33: Requested service option not subscribed 

- #35: PTI already in use 

- #36: Regular deactivation 

- #38: Network failure 

- #39: Reactivation requested 

- #41: Semantic error in TFT 

- #42: Syntactical error in TFT 

- #43: Invalid PDU session identity 

- #44: Semantic errors in packet filters 

- #45: Syntactical error in packet filters 

- #46: Out of LADN service area 

- #50: PDU session type IPv4 only allowed 

- #51: PDU session type IPv6 only allowed 

- #67: Insufficient resources for slice and DNN 

- #68: Not supported SSC mode 

- #81: Invalid PTI value 

- #95: Semantically incorrect message 

- #96: Invalid mandatory information 

- #97: Message type non-existent 

- #98: Message type not compatible 

- #99: IE non-existent 

Check Back-off timer value (T3396, T3584, T3585) 

###### Additional SBI Traces: 

##### 11. Nudm_SubscriberDataManagement (SMF → UDM): 

a. GET /nudm-sdm/v2/{supi}/sm-data?dnn={dnn}&snssai={snssai} 

b. Check response with: 

- sessionAmbr (subscribed AMBR) 

- 5gQosProfile 

- staticIpAddress (if static IP assigned) 

- dnnConfigurations 

##### 12. Npcf_SMPolicyControl (SMF → PCF) - N7: 

a. POST /npcf-smpolicycontrol/v1/sm-policies 

b. Check request with: 

- supi 

- dnn 

- sNssai 

- pduSessionId 

- ipv4Address or ipv6AddressPrefix 

c. Look for 201 Created response with PCC rules: 

- pccRules (Policy and Charging Control rules) 

- sessRules (Session rules) 

- qosDecs (QoS decisions) 

- chgDecs (Charging decisions) 

##### 13. N9 Interface (UPF to UPF) - if multiple UPFs: 

- Check PFCP for intermediate UPF configuration 

- Verify GTP-U tunnel between UPFs 

##### 14. GTP-U Tunnel Verification (N3): 

- Filter gtp.teid in PCAP 

- Verify Echo Request/Response for path management 

- Check G-PDU (user plane data) flow 

- Look for End Marker packets during handover 

- Verify uplink TEID (UPF) and downlink TEID (gNB) 

###### Timing Analysis: 

- Measure time from PDU Session Establishment Request to Accept 

- Typical successful flow: 100-500ms 

- Delays > 2 seconds indicate issues: 

    - SMF processing delay 

    - UPF response delay 

    - Policy decision delay from PCF 

    - gNB resource allocation delay 

###### Common Root Causes: 

- DNN not configured or not subscribed 

- IP address pool exhausted at UPF 

- SMF to UPF N4 association down 

- Incorrect NSSAI configuration 

- QoS profile mismatch 

- PCF policy rejection 

- UPF overload or capacity issues 

- PFCP session establishment failure 

- gNB resource unavailability 

- N3 interface connectivity issues 