#  Inter-RAT HO failures (2G↔3G):

### CHECK:
- Parameters in RNC/BSC, cell neighbor config.

### Troubleshooting Steps: 
- Check neighbor cell relations between 2G and 3G cells 
- Verify handover parameters and thresholds 
- Review measurement reporting configuration 
- Check MSC and BSC/RNC interface availability 
- Verify frequency allocations don't conflict 
- Test handover in both directions separately 
- Review compressed mode configuration (for UMTS measurements) 

 

### PCAP Analysis:
- Look for HO Command/Complete; trace MAP or RANAP HO messages.

### What to Check:
- Look for Measurement Report messages from UE 
- Check RANAP Relocation Required (3G→2G handover) 
- Verify BSSMAP Handover Request (2G→3G handover) 
- Look for Handover Command in both directions 
- Check Handover Complete/Failure messages 
- Verify target cell identification (CGI for 2G, UTRAN cell ID for 3G) 
- Look for PS Handover messages if HSPA active 
- Check cause codes in failure messages: 
- Target cell not available 
- Handover cancelled 
- Timing advance out of range 
- Verify codec re-negotiation during inter-RAT HO 