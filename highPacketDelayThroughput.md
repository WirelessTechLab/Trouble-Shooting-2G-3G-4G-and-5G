# High packet delay/throughput degradation:

### CHECK:
- SGSN/GGSN CPU load, backhaul congestion. 

### Troubleshooting Steps: 
- Check radio network quality and interference 
- Verify transmission network capacity (Gb, Gn interfaces) 
- Check SGSN and GGSN CPU/memory utilization 
- Review QoS configurations and traffic prioritization 
- Test with ping and throughput tools 
- Check for congestion on internet gateway 
- Verify routing and firewall processing delays 

### PCAP Analysis:
- Check RTT, retransmissions in TCP, or GTP-U delay.  

### What to Check:
- Analyze GTP-U tunnel traffic (user plane data) 
- Check RTP stream analysis for voice over GPRS: 
- Packet inter-arrival time 
- Jitter measurements 
- Packet loss percentage 
- Look for TCP retransmissions indicating packet loss 
- Verify Round Trip Time (RTT) between endpoints 
- Check GTP sequence numbers for out-of-order delivery 
- Monitor throughput graphs over time 
- Look for congestion indicators (increasing delays) 
- Verify QoS markings (DSCP/TOS values) 
- Check for fragmentation causing overhead 