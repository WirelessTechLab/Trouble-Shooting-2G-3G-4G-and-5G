# VoNR Registration / Call Setup Failures (IMS over 5G) 

### Troubleshooting Steps: 

###### 1. Verify IMS Registration Over PDU Session (via UPF) 

- Check dedicated IMS PDU session establishment (DNN = "ims") 

- Verify P-CSCF address discovery (PCO or DNS) 

- Check IPSec tunnel establishment (if security association required) 

- Review SIP REGISTER procedures 

- Verify IMS subscription in HSS/UDM 

- Check authentication via AKA (IMS-AKA or 5G-AKA) 

- Review S-CSCF assignment 

##### 2. Check PCF/SMF QoS Enforcement for IMS Slice 

- Verify dedicated IMS slice (S-NSSAI for IMS) 

- Check QoS flow for IMS signaling (5QI=5) 

- Review policy from PCF for IMS services 

- Verify session-AMBR for IMS PDU session 

- Check QoS flow for voice media (5QI=1, GBR) 

- Review priority and pre-emption settings 

###### 3. Review SIP Signaling via P-CSCF/I-CSCF/S-CSCF 

- Check P-CSCF reachability from UE 

- Verify I-CSCF selection and HSS query 

- Review S-CSCF assignment from HSS 

- Check SIP routing and DNS resolution 

- Verify IMS application servers in service chain 

- Review supplementary service invocation 

###### 4. Confirm AMF Supports Emergency and IMS Voice Service 

- Verify AMF IMS voice support capability 

- Check emergency registration support 

- Review voice over PS session indicator 

- Verify IMS voice termination support 

###### 5. Check Fallback Mechanisms 

- Verify EPS Fallback (EPSFB) configuration if VoNR not available 

- Check SRVCC (Single Radio Voice Call Continuity) to 4G/3G 

- Review fallback triggers and conditions 

- Check NG-RAN support for CSFB equivalent 

###### 6. Verify Media Path Establishment 

- Check dedicated bearer/QoS flow for voice (5QI=1) 

- Verify SDP (Session Description Protocol) negotiation 

- Review codec selection (EVS, AMR-WB, AMR-NB) 

- Check RTP/RTCP path establishment 

###### 7. Review IMS Identities 

- Verify IMPI (IMS Private Identity) = IMSI@realm or NAI 

- Check IMPU (IMS Public Identity) = tel: or sip: URI 

- Review MSISDN configuration 

###### 8. Check Emergency Call Support 

- Verify emergency PDU session capability 

- Check emergency registration without authentication 

- Review location information delivery (ESMLC/LMF) 

### PCAP Analysis - What to Check: 

### IMS PDU Session Establishment: 

###### 1. PDU Session Establishment Request (IMS DNN): 

- Capture UplinkNASTransport with PDU Session Establishment Request 

- Check DNN = "ims" (IMS data network name) 

- Verify PDU session type: IPv4, IPv6, or IPv4v6 

- Look for SSC mode = 1 (typically for IMS) 

- Check S-NSSAI dedicated for IMS (e.g., SST=1, SD=specific value) 

- Verify 5GSM capability includes IMS voice support 

###### 2. PCO (Protocol Configuration Options): 

- Look for PCO IE in PDU Session Establishment Request 

- Check for P-CSCF IPv4/IPv6 address request: 

    - Protocol ID: 0x000C (P-CSCF IPv6 address request) 

    - Protocol ID: 0x0001 (P-CSCF IPv4 address request) 

- Look for IM CN Subsystem Signaling Flag: 0x0003 

- Check DNS Server IPv4/IPv6 address request 

###### 3.PDU Session Establishment Accept: 

- Verify PDU Session Establishment Accept received 

- `Check P-CSCF address in PCO response`: 

    - Protocol ID: 0x0001 (P-CSCF IPv4) 

    - Protocol ID: 0x000C (P-CSCF IPv6) 

    - Contains P-CSCF IP address(es) 

- Verify UE IP address allocated 

- Check DNS server addresses 

- `Look for QoS rules for IMS signaling`: 

    - Default QoS flow with 5QI=9 or 5QI=5 

- Verify Session-AMBR appropriate for IMS 

###### 4. DNS Query for P-CSCF (if not in PCO): 

- Capture DNS Query from UE 

- Look for SRV record query: _sip._udp.ims.mnc<MNC>.mcc<MCC>.3gppnetwork.org 

- Or A/AAAA record query if FQDN provided 

- Check DNS Response with P-CSCF addresses 

- Verify priority and weight in SRV records 

##### IPSec Security Association (Optional): 

###### 5. IKEv2 Negotiation (if IPSec used): 

- Capture IKE_SA_INIT request/response (port 500 or 4500) 

- Check proposals: Encryption, integrity, DH group 

- Look for IKE_AUTH request/response 

- Verify EAP-AKA authentication within IKE_AUTH 

- Check Traffic Selectors for SIP traffic 

- Verify ESP Security Association established 

- Look for NAT-T (NAT Traversal) if NAT detected (port 4500) 

###### 6. ESP Encrypted Packets: 

- Look for ESP (protocol 50) packets between UE and P-CSCF 

- Note: SIP messages will be encrypted inside ESP 

- Can identify by IP addresses and SPI (Security Parameter Index)