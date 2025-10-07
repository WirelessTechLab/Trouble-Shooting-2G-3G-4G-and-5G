# Charging and Policy Issues 

### Troubleshooting Steps: 

- Check PCF policy decisions 

- Verify CHF (Charging Function) connectivity 

- Review online vs offline charging 

- Check spending limits and quotas 

- Verify Diameter Ro/Rf or CHF SBI interfaces 

### PCAP Analysis: 

##### Policy Control (N7 - SMF ↔ PCF): 

- Already covered in PDU session establishment 

- Monitor Npcf_SMPolicyControl updates during session 

- Check Event Triggers: 

    - QoS change 

    - RAT type change 

    - User location change 

    - Access type change 

##### Charging (N28, N40, N42): 

- `Offline Charging (CHF via SBI)`: 

    - Capture Nchf_ConvergedCharging_Create request 

    - Check Charging Data Request: 

        - subscriptionId: SUPI, GPSI 

        - nfConsumerIdentification: SMF ID 

        - invocationSequenceNumber: CDR sequence 

        - multipleUnitUsage: Data volumes, time 

    - Verify 201 Created response with charging session 

    - Look for Nchf_ConvergedCharging_Update for interim records 

    - Check Nchf_ConvergedCharging_Release for session termination 

- `Online Charging (via Diameter Ro or CHF)`: 

    - For Diameter Ro, capture CCR-I (Credit-Control-Request Initial) 

    - Check CCR-U (Update) for quota usage 

    - Look for CCA (Credit-Control-Answer) with granted units: 

        - Granted-Service-Unit: Data volume, time 

        - Validity-Time: Quota validity 

    - Verify Multiple-Services-Credit-Control for multiple rating groups 

    - Look for Final-Unit-Indication: Actions when quota exhausted 

    - Check CCR-T (Termination) at session end 

- `Quota Exhaustion`: 

    - Look for CCA with Result-Code: 4012 (DIAMETER_CREDIT_LIMIT_REACHED) 

    - Check Final-Unit-Action: TERMINATE, REDIRECT, RESTRICT_ACCESS 

    - Verify PDU Session Release if terminate action 