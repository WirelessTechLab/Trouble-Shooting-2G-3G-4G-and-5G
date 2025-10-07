# High SDCCH congestion:

### CHECK:
- Paging load, signaling channel usage.

### Troubleshooting Steps:
- Monitor SDCCH allocation and occupancy rates
- Check for SDCCH blocking or seizure failures
- Verify timeslot configuration (SDCCH/4 or SDCCH/8)
- Look for abnormal call holding times on SDCCH
- Check for ghost calls or stuck channels
- Review location update and SMS traffic patterns
- Consider increasing SDCCH capacity

### PCAP Analysis:
- Analyze CM Service Request or Location Update Request not getting accepted.

### What to Check:
- Capture CHANNEL REQUEST on RACH (Random Access Channel)
- Look for IMMEDIATE ASSIGNMENT responses
- Check for IMMEDIATE ASSIGNMENT REJECT (congesti- on indicator)
- Verify SDCCH allocation failures
- Monitor CM SERVICE REQUEST timing on SDCCH
- Check for delayed ASSIGNMENT COMMAND to TCH
- Look for abnormal SCCP connection duration on SDCCH
- Verify T3240 timer expiry (call setup timeout)