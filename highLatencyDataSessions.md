#     High latency on data sessions:

### CHECK:
- Backhaul links, SGSN queue.  

### Troubleshooting Steps: 
- Perform end-to-end latency tests (ping, traceroute) 
- Check radio network quality (RSCP, Ec/Io) 
- Verify transmission network delays 
- Review SGSN and GGSN processing loads 
- Check for congestion on Iu-PS, Gn interfaces 
- Test different APNs and destinations 
- Verify QoS profile application 
 

### PCAP Analysis:
-  Look at TCP retransmissions, RTT spikes. 

### What to Check:
- Analyze ICMP Echo Request/Reply (ping) timing 
- Check TCP three-way handshake duration 
- Measure Round Trip Time (RTT) from various points: 
- UE to SGSN 
- SGSN to GGSN 
- GGSN to internet 
- Look for TCP retransmissions (packet loss indicator) 
- Verify GTP-U tunnel delays 
- Check packet inter-arrival times 
- Monitor jitter in data streams 
- Look for out-of-order packets 
- Check QoS markings and priority handling 
- Verify MTU issues causing fragmentation 
- Analyze window size in TCP for throughput limits 