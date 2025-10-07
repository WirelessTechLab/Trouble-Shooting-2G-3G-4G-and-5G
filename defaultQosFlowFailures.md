# Default QoS Flow Setup Failures (Continued)
### PCAP Analysis - What to Check: (Continued)
### NGAP Messages: (Continued)
##### 15. PDU Session Resource Setup Request: (Continued)
a. Check GBR QoS Flow Information (continued):

- Maximum Packet Loss Rate (uplink/downlink)

- Alternative QoS Parameters Set List (fallback options)

b. Verify Reflective QoS Attribute (RQA):

- Indicates if reflective QoS is enabled

c. Check Additional QoS Flow Information:

- More likely to experience packet loss

d. Look for TSC Traffic Characteristics (Time-Sensitive Communications)

##### 16. PDU Session Resource Setup Response:
a. Look for QoS Flow Setup Response List:

- QFI values successfully established

b. Check QoS Flow Failed to Setup List:

- QFI that failed

- Cause values:

    - Radio resources not available
    -   Failure in the radio interface procedure:
    - Insufficient QoS flow resources
    - QoS flow not supported
    - Invalid QoS combination
    - Unknown QoS flow ID

- NG-RAN Cause: resource not available, unspecified

c. Verify Data Forwarding Response (if applicable):

##### N7 Interface (SMF ↔ PCF):

##### 17. Npcf_SMPolicyControl_Create Request:

a. Capture POST /npcf-smpolicycontrol/v1/sm-policies

b. Check request JSON payload:

- supi: Subscriber identifier

- pduSessionId: PDU session ID

- dnn: Data Network Name

- sNssai: Slice identifier

- pduSessionType: IPv4, IPv6, IPv4v6, Ethernet, Unstructured

- ratType: NR, EUTRA-NR

- ipv4Address or ipv6AddressPrefix: UE IP

- servingNetwork: PLMN ID

- userLocationInfo: Cell ID, TAI

- ueTimeZone: Time zone

- subscriptionData: From UDM

    - sessionAmbr: Subscribed AMBR

    - 5gQosProfile: Subscribed QoS parameters

18. Npcf_SMPolicyControl_Create Response:

a. Look for 201 Created response:

b. Check Location header with policy association URI

c. Verify response JSON body:

- pccRules: Array of PCC rule objects

    - pccRuleId: Unique identifier

    - precedence: Rule priority (1-65535)

    - flowInfos: Traffic filters

        - flowDescription: IP filter syntax

        - flowDirection: DOWNLINK, UPLINK, BIDIRECTIONAL

    - refQosData: Reference to QoS data

    - refChargData: Reference to charging data

- sessRules: Session rules

    - sessRuleId: Session rule identifier

    - authSessAmbr: Authorized session AMBR

        - uplink: Uplink AMBR

        - downlink: Downlink AMBR

    - authDefQos: Authorized default QoS

        - 5qi: 5QI value

        - arp: ARP parameters

    - refCondData: Reference conditions

- qosDecs: QoS decisions map

- Key: Reference ID

- Value: QoS data object

    - qosId: QoS decision ID

    - 5qi: 5QI value

    - maxbrUl: Maximum bitrate uplink

    - maxbrDl: Maximum bitrate downlink

    - gbrUl: Guaranteed bitrate uplink (if GBR)

    - gbrDl: Guaranteed bitrate downlink (if GBR)

    - arp: Allocation retention priority

    - reflectiveQos: true/false

    - qnc: QoS notification control

- chgDecs: Charging decisions

- traffContDecs: Traffic control decisions

- revalidationTime: Policy revalidation time

- online: Online charging enabled

- offline: Offline charging enabled

##### 19. Npcf_SMPolicyControl_Update (Policy Updates):

- Look for POST to policy association update URI

- Check for SmPolicyUpdateNotification:

    - Updated PCC rules

    - QoS flow binding updates

    - Session AMBR modifications

###### 20. Error Responses from PCF:

- 400 Bad Request: Invalid request parameters

- 403 Forbidden: Policy not authorized

- 404 Not Found: Policy context not found

- 500 Internal Server Error: PCF processing error

- 503 Service Unavailable: PCF overload

##### N4 Interface (SMF ↔ UPF):

###### 21. PFCP Session Establishment/Modification - QER Details:

a. Capture Create QER (QoS Enforcement Rule):

- QER ID: Unique identifier

- QER Correlation ID: For grouping

- Gate Status: OPEN (allow traffic), CLOSED (block traffic)

- Maximum Bitrate (MBR):

    - Uplink MBR (in kbps)

    - Downlink MBR (in kbps)

- Guaranteed Bitrate (GBR) (if GBR flow):

    - Uplink GBR (in kbps)

    - Downlink GBR (in kbps)

- QoS Flow Identifier (QFI): 0-63

- Reflective QoS (RQI): true/false

- Paging Policy Indicator: Voice, delay-sensitive

- Averaging Window: Time window for rate measurement`

- QER Control Indications: RCSR (Rate Control Status Reporting)

###### 22. Update QER (During Session Modification):

a. Look for PFCP Session Modification Request:

b.  Check Update QER IE with modified parameters:

- Changed MBR/GBR values

- Gate status changes

- QFI modifications

c. Verify Apply Action in associated FAR

##### 23. PFCP Session Establishment/Modification Response:

-Check Cause value: Request accepted (1):

- Look for Created/Updated QER acknowledgment

- Check for Offending IE if failure

- Look for Load Control Information:

    - Sequence number

    - Metric (CPU, memory utilization)

    - Indicates UPF overload

- Check Overload Control Information:

    - Reduction percentage

    - Period of validity

##### GTP-U User Plane (N3 Interface):

###### 24. GTP-U Extension Header for QFI:

a. Filter gtp protocol in PCAP

b. Check Extension Header field:

- Next Extension Header Type: 0x85 (PDU Session Container)

- PDU Session Container contents:

    - PDU Type: 0 (DL PDU Session Information) or 1 (UL PDU Session Information)

    - QoS Flow Identifier (QFI): Maps packet to QoS flow

    - Reflective QoS Indicator (RQI): If reflective QoS active

    - Paging Policy Presence (PPP): For paging optimization

    - Paging Policy Indicator (PPI): 1-7 (delay sensitive)

c. Example GTP-U header structure:

##### GTP-U Header:  Version: 1  Protocol Type: GTP (1) Extension Header:  Present  Message Type: G-PDU (255)

#####  TEID: 0x12345678  Sequence Number: 1234  Extension Headers:  PDU Session Container:  QFI: 9

#####  (default bearer)  RQI: 0 (no reflective QoS)


###### 25. QoS Flow Mapping Verification:

Correlate QFI in GTP-U packets with QoS rules in NAS

- Verify correct QFI for different traffic types:

    - QFI 1: VoNR (5QI=1)

    - QFI 5: IMS signaling (5QI=5)

    - QFI 9: Default internet (5QI=9)

- Check packet filtering accuracy (correct QFI assignment)

##### 26. DSCP/TOS Marking:`

- Check IP header of encapsulated packets

- Verify DSCP (Differentiated Services Code Point) values:

    - EF (Expedited Forwarding): 46 - for voice

    - AF41: 34 - for video

    - BE (Best Effort): 0 - for default

- Ensure marking preservation through network

#### RRC/SDAP Layer (if available):

###### 27. RRC Connection Reconfiguration:

- Look for DRB (Data Radio Bearer) Configuration

- Check SDAP-Config:

- SDAP-Header presence (UL/DL)

- Default DRB indicator

- Mapped QoS flows:

- QFI list mapped to this DRB

- Verify PDCP-Config for each DRB:

- RLC mode: AM (Acknowledged Mode), UM (Unacknowledged Mode)
- PDCP SN size: 12 or 18 bits

- Header compression: ROHC profile

- Check MAC-CellGroupConfig:

##### Scheduling Request configuration:

- BSR (Buffer Status Report) configuration

- PHR (Power Headroom Report) configuration

###### 28. SDAP Data PDU:

- Check for SDAP header in user plane (if not end-to-end):

- QFI: Maps to 5G QoS flow

- RDI (Reflective QoS Flow to DRB mapping Indication)

- RQI (Reflective QoS Indicator)

##### Monitoring and Statistics:

###### 29. QoS Flow Performance Metrics:
- Monitor packet delay per QoS flow

- Check packet loss rate per QFI

- Verify throughput against MBR/GBR

- Analyze jitter for delay-sensitive flows

- Check out-of-order delivery

###### 30. Resource Utilization:
- Monitor PRB (Physical Resource Block) utilization at gNB

- Check buffer occupancy at UPF

- Verify scheduling priority enforcement

- Review congestion indicators

##### Common Failure Scenarios in PCAP:

###### 1. QoS Not Supported:`
- NGAP: QoS Flow Failed to Setup with cause "QoS 
flow not supported"

Indicates gNB doesn't support requested 5QI or GBR requirements

###### 2. Insufficient Resources:

- NGAP: Cause "radio resources not available"

- PFCP: Load Control Information with high metric

- Indicates resource exhaustion at gNB or UPF

###### 3. Policy Rejection:

- PCF returns 403 Forbidden

- PCC rules exclude requested QoS

- Insufficient subscription for GBR flows

- ###### 4. Configuration Mismatch:

- Requested 5QI not configured on UPF

- QFI range exceeded (> 63)

- AMBR violation (flow exceeds session AMBR)

- ###### 5. Reflective QoS Failure:

- RQI not set in DL packets

- UE doesn't support reflective QoS

- Timer expiry without detecting UL packets

#### Timing Analysis:

- QoS Flow Setup Time: 50-200ms typical

- Policy Decision Time (PCF): < 100ms

- PFCP QER Creation: < 50ms

- NGAP Resource Setup: 100-300ms

- Total delay > 1 second indicates issues

#### Common Root Causes:

- Subscription doesn't include GBR flows

- PCF policy restricts QoS parameters

- gNB lacks radio resources for guaranteed bitrates

- UPF QoS enforcement capability insufficient

- QFI mapping configuration error

- AMBR exhaustion (sum of GBR exceeds AMBR)

- Incorrect 5QI configuration

- Priority level conflicts

- ARP pre-emption failures

- Reflective QoS not supported

