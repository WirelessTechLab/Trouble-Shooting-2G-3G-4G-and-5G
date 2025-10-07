# LOCATION UPDATE FAILURES (HLR/VLR mismatch):

### CHECK:
IMSI authentication, VLR–HLR connectivity, MAP Update Location response.

### Troubleshooting Steps:
- Check HLR and VLR synchronization status

- Verify IMSI provisioning in HLR
- Check MAP connectivity between VLR and HLR
- Review authentication parameters (Ki, authentication triplets)
- Verify VLR capacity and database locks
- Check for SS7/SIGTRAN connectivity issues
- Review HLR subscriber data consistency

### PCAP Analysis:
- Look for MAP UpdateLocation, InsertSubscriberData; check for reject/error codes.
- Capture MAP_UPDATE_LOCATION request from VLR to HLR
- Check MAP_UPDATE_LOCATION response (should return subscriber data)
- Look for MAP error codes (unknown subscriber, roaming not allowed)
- Verify IMSI in location update request
- Check MAP_CANCEL_LOCATION from old VLR
- Verify Insert Subscriber Data message from HLR to VLR
- Check SCCP/TCAP layer for dialogue establishment issues
- Look for timeout messages (no response from HLR)

<br>

![Look for IMSI in location update data request](./Images/Look%20for%20IMSI%20location.png)