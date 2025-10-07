# CALL DROP DURING HANDOVER

### CHECK:
- Radio signal (RxQual, RxLev), HO success rate, MSC logs.

- Check BSC and MSC alarm logs for errors during handover

- Verify neighbor cell relations and handover parameters

- Check transmission link quality between BSC and MSC (A-interface)

- Review handover statistics and success rates per cell Verify MSC pool configuration and resource availability

- Check for RF coverage issues in handover zones

- Analyze MAP signaling for handover command/complete messages<br>
<br>

### PCAP Analysis:
- Verify handover request/ack (MAP/SS7); look for missing or delayed HO Complete.

- Look for BSSMAP Handover Request/Required messages

- Check for Handover Command from MSC to BSS

- Verify Handover Complete message reception
- Check timing between handover request and command (should be < 1-2 seconds)
- Look for SCCP Connection Release indicating premature call drop
- Check for MAP/BSSAP error codes (e.g., resource unavailable)
- Verify A-interface SCCP signaling continuity
- Check for retransmissions indicating transmission issues
<br>

![GSM Handover Signaling Flow](./Images/GSM%20Handover%20Signaling%20Flow.png)

<br>

![Hand Over Failure](./Images/Handover%20Failure.png)