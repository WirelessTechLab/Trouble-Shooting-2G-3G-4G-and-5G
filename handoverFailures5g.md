# Handover Failures (Inter-gNB / Inter-RAT) 

### Troubleshooting Steps: 

###### 1. Check XnAP Handover Signaling Between gNBs 

- Verify Xn interface connectivity between source and target gNB 

- Check SCTP associations on Xn interface 

- Review Xn Setup procedures 

- Verify neighbor cell relations configured 

- Check handover parameters and thresholds 

- Review measurement configurations 

- Verify TNL (Transport Network Layer) addresses 

###### 2. Verify N2 (NGAP) Handover Signaling via AMF 

- Check when Xn handover is not possible (no Xn interface) 

- Verify AMF-initiated handover procedures 

- Review inter-AMF handover scenarios 

- Check N2 interface connectivity 

- Verify AMF handover coordination 

###### 3. Ensure UPF Path Switching (N9 Interface if Multiple UPFs) 

- Check if session involves multiple UPFs (I-UPF, PSA-UPF) 

- Verify N9 interface between UPFs 

- Review path switching procedures 

- Check UPF selection and relocation 

- Verify indirect data forwarding tunnels 

###### 4. Review Slice Continuity (NSSF Slice Allocation) 

- Verify S-NSSAI availability in target cell/area 

- Check NSSF slice selection policies 

- Review allowed vs. configured NSSAI 

- Verify slice continuity across handover 

- Check slice admission control 

###### 5. Verify UE Context Transfer 

- Check complete context transfer between gNBs 

- Review PDU session context information 

- Verify QoS flow context 

- Check security context transfer (NCC, NH) 

- Review RRC configuration transfer 

###### 6. Check Radio Measurements 

- Verify measurement reports from UE 

- Review RSRP (Reference Signal Received Power) 

- Check RSRQ (Reference Signal Received Quality) 

- Verify SINR values 

- Review handover triggering thresholds (A3, A5 events) 

###### 7. Verify Target Cell Resources 

- Check target gNB capacity and load 

- Verify admission control at target 

- Review resource availability 

- Check PRB utilization 

###### 8. Review Handover Types 

- Distinguish Xn-based vs. N2-based handover 

- Check intra-gNB vs. inter-gNB scenarios 

- Verify intra-frequency vs. inter-frequency 

- Review conditional handover (CHO) if configured 

###### 9. Check Data Forwarding 

- Verify GTP-U forwarding tunnels (X2-U/N2-U) 

- Check data forwarding flag configuration 

- Review packet loss during handover 

### PCAP Analysis - What to Check: 

##### Xn-Based Handover (Direct gNB to gNB): 

###### 1. Measurement Report from UE: 

a. Capture RRC MeasurementReport (if RRC traces available) 

b. Check measId: Measurement identity 

c. Verify measResultServingCell: 

- rsrpResult: RSRP of serving cell (0-127) 

- rsrqResult: RSRQ of serving cell (0-127) 

d. Check measResultNeighCells: 

- physCellId: Physical cell ID of neighbor 

- rsrpResult: RSRP of neighbor cell 

- rsrqResult: RSRQ of neighbor cell 

e. Verify A3 event triggered (neighbor becomes offset better than serving) 

f. Check A5 event (serving below threshold1, neighbor above threshold2) 

###### 2. XnAP Handover Request (Source gNB → Target gNB): 

a. Capture XnAP: HandoverRequest message 

b. Check UE Context Information: 

- gNB-CU UE XnAP ID: Source gNB UE identifier 

- UE Security Capabilities: Encryption/integrity algorithms 

- Security Context: NCC (Next hop Chaining Counter), NH (Next Hop) 

- AS Security Information 

- UE History Information: Previous cells 

c. Verify PDU Session Resources to be Setup List: 

- PDU Session ID 

- S-NSSAI 

- QoS Flows to be Setup List: 

    - QFI 

    - QoS Flow Level QoS Parameters 

- UL NG-U UP TNL Information: Source gNB TEID for DL forwarding 

- Security Indication: Integrity/confidentiality required 

d. Check RRC Context: Full UE RRC configuration 

e. Verify Target Cell ID: Global gNB ID + Cell ID 

f. Look for UE Aggregate Maximum Bit Rate 

g. Check Masked IMEISV 

###### 3. XnAP Handover Request Acknowledge (Target gNB → Source gNB): 

a. Look for XnAP: HandoverRequestAcknowledge 

b. Check gNB-CU UE XnAP ID: Target gNB UE identifier (new) 

c. Verify PDU Session Resources Admitted List: 

- PDU Session ID 

- DL NG-U UP TNL Information: Target gNB TEID for UL after HO 

- QoS Flows Admitted List: QFI values 

- Data Forwarding Response: If data forwarding accepted 

    - UL Data Forwarding: Forwarding tunnel info 

    - DL Data Forwarding: Forwarding tunnel info 

d. Check PDU Session Resources Not Admitted List (if any): 

- Cause: Resource not available, Unknown PDU session 

e. Verify RRC Container: RRC Reconfiguration message for UE 

f. Look for Target to Source Transparent Container 

###### 4. RRC Reconfiguration (Source gNB → UE): 

- Capture RRC: RRCReconfiguration with reconfigurationWithSync 

- `Check ReconfigurationWithSync IE`: 

    - Target PhysCellId: Physical cell ID of target 

    - Target ARFCN: Frequency of target cell 

    - T304: Handover timer (starts when UE starts accessing target) 

- `Verify MobilityControlInfo`: 

    - New UE Identity (C-RNTI in target cell) 

    - RACH-ConfigDedicated: Dedicated preamble for contention-free RACH 

- `Check RadioBearerConfig`: 

    - DRB configurations for target 

    - SDAP/PDCP/RLC configurations 

- Verify masterCellGroup: Updated cell group config for target 

###### 5. RRC Reconfiguration Complete (UE → Target gNB): 

- Look for RRC: RRCReconfigurationComplete at target gNB 

- Indicates successful handover execution 

- Timing from Reconfiguration to Complete: typically 50-150ms 

- Delay > 300ms indicates issues (weak signal, RACH failure) 

###### 6. XnAP UE Context Release (Target gNB → Source gNB): 

- Capture XnAP: UEContextRelease 

- Confirms handover completion 

- Source gNB can release resources 

- Check gNB-CU UE XnAP IDs for correlation 

###### 7. XnAP SN Status Transfer (Source → Target): 

- Look for XnAP: SNStatusTransfer 

- Contains PDU Session Resources Subject to Status Transfer List: 

    - PDCP SN (Sequence Numbers) for each DRB 

        - UL PDCP SN: Last received from UE 

        - DL PDCP SN: Next to be transmitted to UE 

    - Receive Status of PDCP SDU: Bitmap of received PDUs 

- Ensures lossless handover (in-sequence delivery) 

###### 8. XnAP Path Switch Request (Target gNB → AMF via N2): 

- Capture NGAP: PathSwitchRequest 

- Sent by target gNB to update user plane path 

- Check Source AMF UE NGAP ID and RAN UE NGAP ID 

- Verify PDU Session Resources to be Switched List: 

    - PDU Session ID 

    - DL NG-U UP TNL Information: New target gNB TEID 

    - QoS Flow Accepted List 

- Look for User Location Information: New cell ID, TAI 

###### 9. NGAP Path Switch Request Acknowledge (AMF → Target gNB): 

- Look for NGAP: PathSwitchRequestAcknowledge 

- Check PDU Session Resources Switched List: 

    - Confirms session continuity 

- Verify UL NG-U UP TNL Information: UPF TEID (unchanged or updated) 

- Confirms user plane path switched successfully 

###### 10. N4 Session Modification (SMF → UPF): 

- Capture PFCP Session Modification Request 

- Check Update FAR (Forwarding Action Rule): 

    - FAR ID 

    - Apply Action: FORW (forward) 

    - Update Forwarding Parameters: 

        - Outer Header Creation: New GTP-U TEID for target gNB 

        - Destination Interface: ACCESS 

- Verify Update PDR if source changed 

- Look for PFCP Session Modification Response with cause = accepted 

###### 11. Data Forwarding (Source gNB → Target gNB): 

- Check GTP-U packets on Xn-U interface (if data forwarding enabled) 

- Look for indirect forwarding tunnel 

- Verify GTP-U TEID for forwarding 

- Check sequence numbers for in-order delivery 

- Monitor End Marker packet: Indicates end of data forwarding 

    - GTP-U Message Type: 254 (End Marker) 

    - Signals no more packets will be forwarded 

##### N2-Based Handover (via AMF - when no Xn interface): 

###### 12. NGAP Handover Required (Source gNB → AMF): 

- Capture NGAP: HandoverRequired 

- Check Handover Type: Intra5GS, FiveGStoEPS, EPS to5GS 

- Verify Cause: Handover desirable for radio reasons, time critical handover 

- Look for Target ID: 

    - Target RAN Node ID: Target gNB identifier 

    - Selected TAI: Target Tracking Area 

- Check PDU Session Resource List: 

    - PDU Session ID 

    - Handover Required Transfer: Contains QoS flows and TNL info 

- Verify Source to Target Transparent Container: RRC context 

###### 13. NGAP Handover Request (AMF → Target gNB): 

- Look for NGAP: HandoverRequest 

- Similar to Xn Handover Request but via AMF 

- Check UE Security Capabilities 

- Verify Security Context 

- Look for Allowed NSSAI for target 

- Check PDU Session Resource Setup List 

###### 14. NGAP Handover Request Acknowledge (Target gNB → AMF): 

- Capture NGAP: HandoverRequestAcknowledge 

- Check PDU Session Resource Admitted List 

- Verify Target to Source Transparent Container: RRC Reconfiguration 

- Look for data forwarding information 

###### 15. NGAP Handover Command (AMF → Source gNB): 

- Look for NGAP: HandoverCommand 

- Contains Target to Source Transparent Container from target 

- Source gNB extracts RRC Reconfiguration for UE 

- Check PDU Session Resource Handover List 

###### 16. NGAP Handover Notify (Target gNB → AMF): 

- Capture NGAP: HandoverNotify after UE completes handover 

- Check User Location Information: New cell, new TAI 

- Confirms successful handover execution 

- AMF updates UE location 

###### 17. NGAP UE Context Release Command (AMF → Source gNB): 

- Look for NGAP: UEContextReleaseCommand 

- AMF instructs source gNB to release UE context 

- Check Cause: Successful handover 

###### 18. NGAP UE Context Release Complete (Source gNB → AMF): 

- Capture NGAP: UEContextReleaseComplete 

- Source gNB confirms resource release 

##### Inter-AMF Handover: 

###### 19. N14 Interface (AMF to AMF): 

- Look for Namf_Communication_CreateUEContext Request (Source AMF → Target AMF) 

- Check UE Context transfer: 

    - SUPI 

    - PEI 

    - Allowed NSSAI 

    - UE Security Context 

    - Location Info 

- Verify 201 Created response from target AMF 

###### 20. N11 Context Transfer (SMF involvement): 

- Check Nsmf_PDUSession_UpdateSMContext 

- SMF updates session association with new AMF 

- Verify targetServingNfId: New AMF identifier 

##### Inter-RAT Handover (5G ↔ 4G): 

###### 21. 5G to EPS Handover: 

- Look for NGAP: HandoverRequired with targetID = EPS 

- Check Source to Target Transparent Container: Contains E-UTRAN info 

- Verify PDU Session to E-RAB mapping 

- Look for S1AP: HandoverRequest on S1 interface (AMF to MME via N26) 

- Check Forward Relocation Request on S10 (if no N26) 

###### 22. EPS to 5G Handover: 

- Capture S1AP: HandoverRequired from eNB 

- Look for Forward Relocation Request (MME to AMF) 

- Check NGAP: HandoverRequest to target gNB 

- Verify E-RAB to PDU Session mapping 

##### Handover Failure Scenarios: 

###### 23. XnAP/NGAP Handover Preparation Failure: 

a. Look for XnAP: HandoverPreparationFailure or NGAP: HandoverPreparationFailure 

b. Check Cause values: 

- `Radio Network Layer Causes`: 

    - Resource not available (general) 

    - Cell not available 

    - Unknown target ID 

    - No radio resources available in target cell 

    - Invalid QoS combination 

    - Encryption and/or integrity protection algorithms not supported 

    - Failure in the radio interface procedure 

    - Release due to handover cancellation 

- `Transport Layer Causes`: 

    - Transport resource unavailable 

    - Unspecified 

- `Protocol Causes`: 

    - Transfer syntax error 

    - Abstract syntax error 

    - Message not compatible with receiver state 

- `Miscellaneous Causes`:   - 

    - Control processing overload 

    - Hardware failure 

    - Not enough user plane processing resources 

    - Unspecified failure 

###### 24. Handover Cancel: 

- Look for XnAP: HandoverCancel or NGAP: HandoverCancel 

- Sent by source when handover needs to be aborted 

- Check Cause: TX2RELOCoverall timer expiry, successful handover, etc. 

###### 25. RRC Re-establishment: 

- Capture RRC: RRCReestablishmentRequest from UE 

- Indicates handover failure at radio level 

- Check reestablishmentCause: Handover failure, reconfiguration failure 

- Look for RRC: RRCReestablishment from network (success) or RRC: RRCReestablishmentReject (failure) 

- If reject, UE returns to RRC_IDLE 

###### 26.  NGAP Error Indication: 

- Look for NGAP: ErrorIndication 

- Check Cause for handover-related errors 

- Indicates protocol or procedural errors 

##### Timing and Performance Analysis: 

###### 27. Handover Execution Time: 

- Measure time from RRC Reconfiguration to RRC Reconfiguration Complete 

- Typical values: 50-150ms 

- Includes: 

    - UE processing time 

    - RACH procedure in target cell 

    - Random access delay 

- T304 timer value (in RRC Reconfiguration): 50ms to 2000ms 

    - If UE doesn't complete before T304 expiry → Handover failure 

###### 28. Handover Interruption Time: 

- Measure data plane interruption (last packet in source to first packet in target) 

- Target: < 50ms for intra-frequency 

- Target: < 70ms for inter-frequency 

- Look for GTP-U packet timestamps 

###### 29. Path Switch Delay: 

- Measure from Path Switch Request to Path Switch Request Ack 

- Typical: 50-200ms 

- Includes SMF/UPF update time 

###### 30. Data Forwarding Window: 

- Time between handover command and End Marker 

- Check number of forwarded packets 

- Verify no packet loss (compare sequence numbers) 

##### Multi-UPF Scenarios (N9 Interface): 

###### 31. UPF Path Switch via N9: 

- If session uses I-UPF (intermediate) and PSA-UPF (anchor): 

    - Check N4 Session Modification to I-UPF 

    - Verify new target gNB TEID in I-UPF FAR 

    - PSA-UPF may remain unchanged (sends via I-UPF) 

- If UPF relocation needed: 

    - Look for new N4 session with new PSA-UPF 

    - Check N9 tunnel establishment between UPFs 

    - Verify data path: gNB ↔ new UPF ↔ old UPF (during transition) ↔ DN 

###### 32. ULCL/Branching Point: 

- If Uplink Classifier (ULCL) or Branching Point used: 

    - Check traffic steering updates 

    - Verify N9 tunnel modifications 

##### Slice Continuity: 

###### 33. S-NSSAI Availability Check: 

- Verify Allowed NSSAI in handover messages 

- Check if target supports same S-NSSAI 

- Look for NSSAI unavailable in reject causes 

- If slice not available in target: 

    - PDU session may be released 

    - Or UE may be rejected from cell 

###### 34. NSSF Query (if applicable): 

- Check Nnssf_NSSelection queries 

- Verify slice availability in target TA/cell 

- Look for slice admission control decisions 

##### Common Root Causes: 

- Target cell resource exhaustion 

- Weak radio conditions in handover zone 

- Xn/N2 interface connectivity issues 

- Incorrect neighbor cell configuration 

- Handover parameter misconfiguration (thresholds too aggressive/conservative) 

- Security context transfer failure 

- QoS resources unavailable in target 

- Slice not available in target area 

- UPF path switch failure 

- Data forwarding tunnel failure 

- RRC reconfiguration timeout (T304) 

- AMF overload delaying handover 

- Inter-vendor interoperability issues 

- Missing or incorrect transparent containers