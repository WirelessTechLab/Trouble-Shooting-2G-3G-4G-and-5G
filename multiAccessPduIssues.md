# Multi-Access PDU (MA PDU) Session Issues 

### Troubleshooting Steps: 

- Check MA PDU session support in UE and network 

- Verify ATSSS (Access Traffic Steering, Switching, Splitting) configuration 

- Review 3GPP and non-3GPP access coordination 

- Check policy from PCF for traffic steering 

- Verify UPF support for ATSSS 

### PCAP Analysis: 

- Look for MA PDU Session Request indicator in PDU Session Establishment 

- Check MA PDU Session Information IE 

- Verify ATSSS Capability in UE and network 

- Look for Access Type indicators: 3GPP_ACCESS, NON_3GPP_ACCESS 

- Check N4 Session Establishment for both access types 

- Verify Steering Mode: Active-Standby, Smallest Delay, Load Balancing, Priority-based 

- Look for PMF (Packet Marking Function) and MPTCP proxy configuration 

- Check Traffic Steering Policy from PCF on N7 