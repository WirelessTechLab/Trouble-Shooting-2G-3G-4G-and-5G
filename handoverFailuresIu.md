#   Handover failures (Iu-PS/Iu-CS): 

### CHECK:
- RNC interconnection, MME/SGSN interaction. 

### Troubleshooting Steps: 
- Check RNC and SGSN/MSC interface status 
- Verify handover parameters and thresholds 
- Review radio measurement reports 
- Check target cell availability 
- Verify GTP tunnel relocation procedures 
- Review RANAP signaling for errors 
- Check for resource availability at target 
 

### PCAP Analysis:
-  Look for RANAP Relocation Request/Command/Failure. 

### What to Check:
- Look for RANAP Relocation Required from source RNC 
- Check RANAP Relocation Request to target RNC 
- Verify Relocation Request Acknowledge from target 
- Look for Relocation Command back to source RNC 
- Check Relocation Complete message 
- Verify cause codes in failure scenarios: 
- Relocation preparation failure 
- Relocation failure in target 
- Relocation cancelled 
- For Iu-PS: Check SRNC Relocation Info IE 
- Look for GTP-C Update PDP Context during SRNS relocation 
- Check Forward SRNS Context for PDP state transfer 
- Verify new GTP TEID assignment after relocation 