# Roaming Issues (Home-Routed vs Local Breakout) 

### Troubleshooting Steps: 

- Identify roaming scenario: Home-routed, Local Breakout, or LBO with HR 

- Check visited network AMF/SMF selection 

- Verify home network connectivity (N9, N32, S8-HR) 

- Review roaming agreements and SEPP configuration 

- Check DNS/NRF resolution for home network NFs 

- Verify charging and policy control in roaming 

### PCAP Analysis: 

##### Home-Routed Roaming: 

- Look for Visited PLMN in Registration Request 

- Check AMF in visited network handles registration 

- Verify Nudm queries go to Home UDM (via SEPP) 

- Look for Home SMF selection for PDU session 

- Check N9 interface between visited UPF and home UPF 

- Verify S-SEPP (visited) to H-SEPP (home) communication on N32 

- Look for N32-f (forwarding) for SBI messages 

- Check Token-based authentication on N32 

##### Local Breakout: 

- Verify Visited SMF selected for PDU session 

- Check Visited UPF provides local internet breakout 

- Look for Visited PCF involvement in policy control 

- Verify Home SMF+PCF involvement may still occur 

- Check Charging handled by visited network 

##### SEPP Security: 

- Capture TLS handshake on N32 interface 

- Verify certificate exchange between SEPPs 

- Check JWT (JSON Web Token) in HTTP headers for API protection 

- Look for Topology Hiding: Private IP addresses replaced 

- Verify Message filtering and modification by SEPP 