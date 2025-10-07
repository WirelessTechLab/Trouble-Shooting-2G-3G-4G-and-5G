# High packet loss/delay (SGi/Internet Side)

### Check: 
PGW–internet link, firewall/NAT. 

### Troubleshooting Steps: 

- - Test connectivity from PGW to internet 

- Check PGW CPU and bandwidth utilization 

- Verify SGi interface capacity 

- Review routing and NAT configuration 

- Check for congestion at internet gateway 

- - Test different destinations and services 

- Verify firewall and security appliance performance 

### PCAP: 
TCP retransmissions, out-of-order packets. 

### What to Check: 

- Capture traffic on SGi interface (PGW to internet) 

- Perform ping tests and analyze RTT 

- Check TCP retransmissions percentage 

- Analyze packet inter-arrival time 

- Look for out-of-order packets 

- Verify MTU and fragmentation issues 

- Check ICMP unreachable or timeout messages 

- Monitor throughput degradation over time 

- Analyze jitter for real-time applications 

- Look for TCP zero window conditions (congestion) 

- Check packet loss rate (should be < 0.5%) 

- Verify QoS markings preservation through network 

- Look for blackhole routing (packets not returning) 