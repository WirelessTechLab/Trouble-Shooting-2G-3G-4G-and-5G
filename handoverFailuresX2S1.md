# Handover failures (X2/S1): 

### Check: 
eNB neighbor config. 

### Troubleshooting Steps: (continued) 

- Check MME capacity for S1 handovers 

- Verify GTP tunnel relocation on SGW 

- Review handover success/failure statistics per cell pair 

- Check radio conditions in handover zone 

- Test with stationary UE vs. high-speed mobility 

 

### PCAP: 
Look for Handover Request/Ack, Path Switch failures. 

### What to Check: 

##### For X2 Handover: 

- Look for Measurement Report from UE (RRC message) 

- Check X2AP Handover Request from source to target eNodeB 

- Verify Handover Request Acknowledge from target eNodeB 

- Look for RRC Connection Reconfiguration with mobility control info 

- Check RRC Connection Reconfiguration Complete at target 

- Verify X2AP UE Context Release from target to source 

- Look for Path Switch Request from target eNodeB to MME 

- Check Path Switch Request Acknowledge from MME 

- Verify Modify Bearer Request/Response for GTP tunnel update 

##### Look for X2 Handover Preparation Failure with causes: 

- Radio resources not available 

- Target cell not available 

- No radio resources available in target cell 

- Invalid MME Group ID 

- Check X2 Handover Cancel messages 

- Verify SCTP associations on X2 interface 

- Look for S1 Release if X2 HO fails and falls back to S1 

##### For S1 Handover: 

- Capture S1AP Handover Required from source eNodeB to MME 

- Check S1AP Handover Request from MME to target eNodeB 

- Verify Handover Request Acknowledge from target 

- Look for Handover Command from MME to source eNodeB 

- Check Handover Notify from target eNodeB after successful HO 

- Look for S1AP Handover Failure with cause codes: 

- No radio resources available 

- Unknown target ID 

- Target not allowed 

- Verify Forward Relocation Request/Response (if inter-MME) 

- Check Create Indirect Data Forwarding Tunnel messages 

- Look for GTP-U data forwarding during handover 

- Verify Release Resource from source eNodeB