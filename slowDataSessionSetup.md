#    Slow data session setup: 

### CHECK:
- DNS resolution, SGSN processing delay. 

### Troubleshooting Steps: 
- Measure time from attach to PDP context activation 
- Check SGSN processing delays 
- Verify HLR query response times 
- Review DNS resolution timing 
- Check GGSN response times 
- Verify radio bearer establishment timing 
- Review network congestion indicators 
 

### PCAP Analysis:
-  Delay between Create PDP Req → Resp.  

### What to Check:
- Timestamp analysis of complete session setup flow: 
- Attach Request → Attach Accept 
- Authentication timing 
- Activate PDP Context Request → Accept 
- Create PDP Context Request → Response 
- RAB Assignment Request → Response 
- Look for delays between messages (> 2-3 seconds abnormal) 
- Check for retransmissions indicating packet loss 
- Verify DNS query timing for APN resolution 
- Look for HLR query delays (MAP Send Auth Info) 
- Check GGSN processing time (Create PDP response delay) 
- Monitor RRC connection establishment timing 
- Verify RAB establishment delays 
- Look for timer expiries (T3380, T3390, etc.) 