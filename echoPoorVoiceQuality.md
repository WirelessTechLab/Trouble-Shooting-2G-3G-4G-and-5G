# Echo/poor voice quality:

### CHECK:
- Codec mismatch, echo canceller, jitter.

### Troubleshooting Steps:
- Check codec negotiation between MS, BSS, and MSC 
- Verify transcoding unit (TRAU) functionality 
- Check echo canceller configuration on MSC/MGW 
- Review A-interface codec parameters 
- Test with different mobile devices to isolate issue 
- Check for acoustic echo vs. network echo 
- Verify TFO (Tandem Free Operation) configuration 

### What to Check:
- Look for ASSIGNMENT COMMAND with codec information 
- Check Speech Version field in BSSMAP messages 
- Verify codec list in assignment request/complete 
- Look for codec mismatch between requested and assigned 
- Check RTP stream analysis (if IP-based A-interface): 
- Packet loss percentage 
- Jitter values 
- Out-of-order packets 
- Verify TFO/TrFO negotiation in BICC/SIP messages 
- Check for AMR codec rate adaptation issues 