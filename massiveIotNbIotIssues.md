# Massive IoT / NB-IoT Registration Issues 

### Troubleshooting Steps: 

- Check Control Plane CIoT 5GS Optimization support 

- Verify User Plane CIoT 5GS Optimization 

- Review small data transmission configuration 

- Check PSM (Power Saving Mode) settings 

- Verify eDRX (extended DRX) configuration 

- Review connection establishment cause 

### PCAP Analysis: 

- Look for Control Plane CIoT 5GS Optimization in Registration Request 

- Check User Plane CIoT 5GS Optimization support 

- Verify Data over NAS (small data in NAS messages) 

- Look for PDU Session Status IE showing suspended sessions 

- Check PSM Timer values (T3324, T3412) 

- Verify eDRX parameters for extended sleep 

- Look for RRC Release with suspend indicator 

- Check Service Request with data transport 

- Verify NAS message priority for MO exception data 