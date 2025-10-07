# S1/S11/S5 interface failures: (MME–SGW–PGW) 

### Check: 
GTP tunnel creation, SGW/PGW availability. 

### Troubleshooting Steps: 

- Check SCTP associations on S1-MME interface 

- Verify GTP-C tunnel establishment on S11, S5/S8 

- Review interface statistics and error counters 

- Check IP connectivity between nodes 

- Verify diameter protocol on S6a interface 

- Review routing tables and firewall rules 

- Check for interface resets or outages 


### PCAP:-  
Missing Create Session/Modify Bearer responses. 

### What to Check: 

##### For S1-MME: 

- Monitor SCTP INIT/INIT-ACK messages 

- Look for S1 Setup Request/Response 

- Check SCTP heartbeat messages for keep-alive 

- Verify SCTP abort conditions 

- Look for S1AP error indications 

##### For S11: 

- Check Echo Request/Response (GTP-C keep-alive) 

- Verify GTP-C version (version 2) 

- Look for path failure detection 

- Check sequence numbers for message correlation 

#####   For S5/S8: 

- Same as S11 (GTP-C protocol) 

- Verify inter-PLMN connectivity (if roaming) 

##### Common checks: 

- Look for ICMP unreachable messages 

- Check packet retransmissions 

- Verify IP fragmentation issues 

- Monitor interface reset procedures 

- Look for timeout errors 