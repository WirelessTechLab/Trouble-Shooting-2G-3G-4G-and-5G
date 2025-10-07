#   High CS call drop rate: (High Call Drop Rate Due to RNC Congestion):

### CHECK:
- RNC load, Iu-CS congestion. 

### Troubleshooting Steps: 
- Monitor RNC CPU and memory utilization 
- Check RNC call processing capacity vs. actual load 
- Review IuB interface capacity (to NodeBs) 
- Verify Iu-CS/Iu-PS interface capacity 
- Check for software bugs or need for upgrades 
- Review resource allocation policies 
- Consider RNC hardware expansion 
 

### PCAP Analysis:
- Look for abnormal call release with cause values. 

### What to Check:
- Look for RANAP Iu Release Request from RNC with cause "congestion" 
- Check RAB Release Request messages 
- Verify cause codes: 
- Processing overload 
- Equipment failure 
- Resource not available 
- Monitor SCCP connection establishment rate 
- Look for SCCP connection refusal due to congestion 
- Check timing of call drops (correlation with traffic peaks) 
- Verify RANAP Error Indication messages 
- Look for Iu interface reset procedures 
- Monitor SCTP stream saturation indicators 