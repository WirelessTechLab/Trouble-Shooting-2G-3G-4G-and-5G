# NRF (Network Repository Function) Issues 

### Troubleshooting Steps: 

- Check NRF service registration by NFs 

- Verify NRF discovery responses 

- Review NF heartbeat and status updates 

- Check NF profile updates 

### PCAP Analysis: 

- `NF Registration`: 

    - Capture Nnrf_NFManagement_NFRegister (PUT request) 

    - Check NFProfile in request body: 

        - nfInstanceId: UUID 

        - nfType: AMF, SMF, UPF, PCF, etc. 

        - nfStatus: REGISTERED, SUSPENDED 

        - heartBeatTimer: Heartbeat interval (seconds) 

        - fqdn, ipv4Addresses, ipv6Addresses 

        - capacity, load, priority 

        - sNssais: Supported slices 

        - nfServices: Service endpoints 

    - Verify 200 OK or 201 Created response 

- `NF Heartbeat`: 

    - Look for PATCH to NF profile URI 

    - Or Nnrf_NFManagement_NFStatusNotify 

    - Sent periodically per heartBeatTimer 

- `NF Discovery`: 

    - Already shown in UPF selection 

    - Similar for discovering other NF types 

- `NF Deregistration`: 

    - Capture DELETE to NF profile URI 

    - Or implicit deregistration after heartbeat timeout 