# URLLC (Ultra-Reliable Low Latency Communication) Issues 

### Troubleshooting Steps: 

- Verify URLLC slice configuration (S-NSSAI) 

- Check 5QI values for URLLC (e.g., 82, 83, 84, 85) 

- Review packet delay budget (PDB) requirements (< 10ms) 

- Verify packet error rate (PER) targets (10^-6 or better) 

- Check redundant transmission configuration 

- Review TSN (Time-Sensitive Networking) integration if applicable 

### PCAP Analysis: 

- Look for 5QI values indicating URLLC: 

    - 82: Discrete automation (low latency, GBR) 

    - 83: Discrete automation (low latency, non-GBR) 

    - 84: Intelligent transport systems 

    - 85: V2X messages 

- Check Packet Delay Budget: < 10ms typically 

- Verify Packet Error Rate: 10^-6 or 10^-5 

- Look for Redundant transmission indicators in QoS flows 

- Monitor end-to-end latency in packet timestamps 

- Check jitter (should be minimal, < 1ms) 

- Verify QoS Notification Control for URLLC 

- Look for Alternative QoS parameters for fallback 