# TCH CONGESTION (TRAFIC CHANEL AVAILABILTY)

### Check: 
- TRX capacity, channel allocation failures, BSC congestion.

### Troubleshooting Steps:
- Check real-time TCH utilization per cell
- Review cell traffic statistics and peak hour patterns
- Verify TRX configuration and available TCH slots
- Check for hardware failures (TRX, carriers)
- Analyze call blocking rates and assignment failures
- Consider frequency reuse and interference issues
- Evaluate need for capacity expansion

### PCAP Analysis
- See assignment command/complete; check if channel request is rejected due to “no resources.”

### What to Check:

- Look for ASSIGNMENT REQUEST from MSC to BSS
- Check for ASSIGNMENT FAILURE messages with cause codes
- Verify cause code = "no radio resource available" (0x2F)
- Check Channel Activation messages on Abis interface
- Monitor IMMEDIATE ASSIGNMENT REJECT on CCCH
- Look for RACH congestion indicators
- Check timing of assignment attempts vs. failures