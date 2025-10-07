# Multi-Homing and UPF Selection Issues 

### Troubleshooting Steps: 

- Check UPF pool configuration 

- Verify UPF selection criteria (locality, load, capabilities) 

- Review I-UPF (intermediate) and PSA-UPF (anchor) roles 

- Check N9 interface between UPFs 

- Verify NRF-based UPF discovery 

### PCAP Analysis: 

- `Look for Nnrf_NFDiscovery_Request for UPF discovery`: 

    - target-nf-type: UPF 

    - requester-nf-type: SMF 

    - dnn: Data network name 

    - snssai: Slice identifier 

    - target-nf-instance-id: Specific UPF (if known) 

- `Check NFProfile in discovery response`: 

    - nfInstanceId: UPF identifier 

    - nfType: UPF 

    - fqdn: UPF domain name 

    - ipv4Addresses / ipv6Addresses: UPF IPs 

    - sNssais: Supported slices 

    - locality: Geographic location 

    - priority: Selection priority 

    - capacity: Current capacity 

    - load: Current load 

    - nfServices: N4 interface details 

- `Multi-UPF Session`: 

    - Check N4 Session Establishment to I-UPF 

    - Verify FAR in I-UPF points to PSA-UPF via N9 

    - Look for N4 Session Establishment to PSA-UPF 

    - Check N9 GTP-U tunnel between I-UPF and PSA-UPF 

    - Verify traffic flow: gNB → I-UPF (N3) → PSA-UPF (N9) → DN (N6)