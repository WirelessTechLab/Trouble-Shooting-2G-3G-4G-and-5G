# Extended call setup times: 

### Check: 
Redirection delays. 

### Troubleshooting Steps: 

- Measure time from call initiation to alerting/connect 
 
- Break down delays by procedure (CSFB, redirection, call setup) 
 
- Check paging response times 
 
- Verify radio measurements and cell reselection timing 

- Review MSC call processing delays 

- Check transmission delays between network elements 

- Compare redirection vs. handover methods for performance 

- Test during different network load conditions 

 

### PCAP: 
Delay between CSFB initiation and call setup. 

### What to Check: 

##### Timestamp analysis of complete CSFB call flow: 

- Extended Service Request (UE initiates CSFB) 
 
- Time to RRC Connection Reconfiguration (redirection command) 

- Time to detach from LTE and attach to 2G/3G 

- Time to CM Service Request in target RAT 

- Time to SETUP message (call control) 

- Time to Call Proceeding 

- Time to Alerting (remote party ringing) 

- Time to Connect (call answered) 

##### Key timing checkpoints: 

- SGs paging delay (should be < 2 seconds) 

- Service Request to RRC Reconfiguration (< 1 second) 

- Redirection execution time (2-5 seconds typical) 

- LAU completion after landing in 2G/3G (< 3 seconds) 

- Call setup after LAU (3-5 seconds) 

- Total time from dial to alerting (< 15 seconds acceptable) 

##### Look for specific delays: 

- Measurement gaps before CSFB decision 
 
- SGs interface message delays 
 
- RRC message processing delays 

- Frequency scanning in target RAT 

- Authentication procedures in target network 

- MSC call processing time 

- SIP/ISUP signaling delays (if applicable) 

##### Check for issues causing delays: 

- Multiple paging attempts (UE not responding) 

- Timer expiries requiring retransmissions 

- Authentication failures requiring retry 

- LAU rejections requiring retry 

- CM Service Request rejection 

- Slow BSSMAP/RANAP signaling 

- SS7 signaling delays 