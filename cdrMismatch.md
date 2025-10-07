# CDR mismatch: (CDR Generation Mismatch for Billing) 

### Check: 
PGW billing (Gy/Gz). 

### Troubleshooting Steps: 

- Check CDR generation settings on PGW 

- Verify CGF (Charging Gateway Function) connectivity 

- Review Diameter Rf/Ro interface operation 

- Check CDR triggers (volume, time, QoS change) 

- Verify CDR file transfer and mediation 

- Review charging rules in PCRF 

- Check for CDR sequence gaps 

### PCAP: 
Look for CCR/CCA in Diameter. 

### What to Check: 

##### Capture Diameter Accounting Request (ACR) messages on Gz/Rf interface: 

- ACR Start (session begin) 

- ACR Interim (periodic updates) 

- ACR Stop (session end) 

- Verify Accounting Answer (ACA) from CGF 

- Check CDR fields: 

- IMSI 

- MSISDN 

- PGW address 

- APN 

- Data volumes (uplink/downlink) 

- QoS applied 

- Session duration 

- Timestamps 

- Look for missing ACR messages (sequence gaps) 

- Verify charging ID consistency 

- Check partial CDRs during long sessions 

- Look for CDR closure triggers: 

- Volume threshold 

- Time limit 

- QoS change 

- Tariff change 

- Verify correlation between GTP-C sessions and CDRs 

- Check Diameter result codes for accounting 