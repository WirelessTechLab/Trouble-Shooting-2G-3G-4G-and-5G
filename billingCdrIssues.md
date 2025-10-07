# Billing/CDR issues: (CDRs Not Generated):

### CHECK:
- GGSN/SGSN CDR generation, mediation system. 

### Troubleshooting Steps: 
- Check CDR generation settings on SGSN/GGSN 
- Verify CGF (Charging Gateway Function) connectivity 
- Check disk space and CDR file transfer mechanisms 
- Review CDR triggers and thresholds 
- Verify GTP' protocol operation (if used) 
- Check mediation system connectivity 
- Review billing system integration   

### PCAP Analysis:
- Not visible in real-time PCAP, but you can trace GTP-U data and charging (Gy/Gz) messages.

### What to Check:
- Capture GTP' (GTP prime) messages between GGSN/SGSN and CGF 
- Look for Data Record Transfer Request 
- Check Data Record Transfer Response 
- Verify CDR sequence numbers for missing records 
- Look for CDR fields: IMSI, PDP address, volume counters, timestamps 
- Check charging ID correlation between multiple CDRs 
- Verify partial CDR generation during long sessions 