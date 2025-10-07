#   Voice quality issues (AMR, jitter):

### CHECK:
- Codec mode adaptation, transmission delay. 

### Troubleshooting Steps: 
- Check AMR codec mode-set configuration 
- Verify transcoding resources on MSC/MGW 
- Review radio conditions and BLER (Block Error Rate) 
- Check IP network quality on Iu-CS interface (if VoIP) 
- Test with different UE models 
- Verify echo cancellation settings 
- Review jitter buffer configuration 

 

### PCAP Analysis:
- Inspect RTP stream jitter/delay/loss, codec negotiation.

### What to Check:
- Check AMR codec modes in RAB Assignment 
- Look for codec mode-set (e.g., 12.2, 7.4, 5.9, 4.75 kbps) 
- Analyze RTP stream (if IP-based Iu-CS): 
- Jitter values (should be < 30ms) 
- Packet loss (should be < 1%) 
- Maximum delta (packet delay variation) 
- Out-of-sequence packets 
- Check RTP SSRC and payload type 
- Look for AMR comfort noise (SID) frames 
- Verify RTP timestamp consistency 
- Check for IP fragmentation affecting voice packets 
- Monitor QoS markings (EF class for voice) 
- Look for RTCP packets with quality reports  