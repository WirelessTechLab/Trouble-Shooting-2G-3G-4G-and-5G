# Non-3GPP Access Issues (Wi-Fi, Wireline) 

### Troubleshooting Steps: 

- Check N3IWF (Non-3GPP Interworking Function) for untrusted Wi-Fi 

- Verify W-AGF (Wireline Access Gateway Function) for wireline 

- Review IPSec tunnel establishment (UE to N3IWF) 

- check NWu interface configuration 

- Verify registration over non-3GPP access 

- Review access selection and traffic steering 

### PCAP Analysis: 

##### Untrusted Non-3GPP (e.g., Wi-Fi via N3IWF): 

- Capture IKEv2 exchange between UE and N3IWF 

- Check IKE_SA_INIT: Proposals, DH key exchange 

- Look for IKE_AUTH: EAP-5G authentication 

- Verify EAP-5G-Start from N3IWF 

- Check EAP-Identity with SUCI or 5G-GUTI 

- Look for NAS messages tunneled in EAP-5G 

- Verify Registration Request with: 

    - Access Type: NON_3GPP_ACCESS 

    - N3IWF identifier in additional fields 

- Check IPSec ESP tunnel establishment 

- Look for Child SA (Security Association) for user plane 

- Verify NAS messages over IPSec to AMF via N3IWF 

##### Trusted Non-3GPP (TNGF): 

- Similar flow but without full IKEv2 (simplified) 

- Check N2 connection from TNGF to AMF 

- Verify NAS PDU forwarding 

#####   Wireline (W-AGF): 

- Look for PPPoE or IPoE session establishment 

- Check W-CP (Wireline Control Plane) procedures 

- Verify Registration Request over N2 from W-AGF