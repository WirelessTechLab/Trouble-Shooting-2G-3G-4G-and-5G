# GPRS Attach/Detach failures:

### CHECK:
- IMSI authentication, SGSN–HLR interaction. 

### Troubleshooting Steps: 
- Check SGSN capacity and performance 
- Verify HLR connectivity and subscriber provisioning 
- Check authentication procedures (RAND, SRES) 
- Review GPRS subscription data in HLR 
- Verify routing area configuration 
- Check for SIM card issues or IMSI blocks 
- Review detach procedures (network vs. MS initiated)  

### PCAP Analysis:
- Look for Attach Request/Accept or Reject with cause value. 

### What to Check:
- Look for ATTACH REQUEST from MS to SGSN 
- Check ATTACH ACCEPT/REJECT from SGSN 
- Verify GMM cause codes in reject messages: 
- GPRS services not allowed 
- IMSI unknown in HLR 
- Network failure 
- Capture MAP_SEND_AUTHENTICATION_INFO to HLR 
- Check authentication vectors (RAND, SRES, Kc) 
- Look for DETACH REQUEST and its type (power off, normal) 
- Verify P-TMSI allocation in attach accept 
- Check Routing Area Update procedures 