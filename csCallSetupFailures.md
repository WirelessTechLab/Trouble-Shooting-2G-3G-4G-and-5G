# CS call setup failures:

### CHECK:
- RNC–MSC signaling, authentication.

### Troubleshooting Steps: 
- Check RNC and MSC alarm logs 
- Verify Iu-CS interface connectivity and SCTP associations 
- Review call setup timers and parameters 
- Check radio bearer establishment on Uu interface 
- Verify MSC capacity and call processing resources 
- Review RANAP signaling procedures 
- Check for codec negotiation issues 

### PCAP Analysis:
- Verify SETUP, CALL PROCEEDING, ALERTING, CONNECT messages. Missing message = cause.

### What to Check:
- Capture RANAP Initial UE Message (call setup from RNC to MSC) 
- Look for CM SERVICE REQUEST within Initial UE Message 
- Check RANAP Common ID for IMSI binding 
- Verify RAB Assignment Request from MSC to RNC 
- Look for RAB Assignment Response (success or failure) 
- Check failure cause codes in RANAP messages: 
- Radio resource not available 
- Network failure 
- User equipment failure 
- Verify SCCP connection establishment on Iu-CS 
- Look for Direct Transfer messages carrying call control 
- Check codec information in RAB parameters 
- Monitor call proceeding/alerting/connect messages 