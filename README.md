# SIEM Detection Engineering & Alert Tuning Playbook

## Purpose
This repository demonstrates practical detection engineering, alert tuning, and investigation workflows. The focus is on reducing false positives, improving signal quality, and supporting effective incident response.

## Scope
- Detection rule design (Sigma + Microsoft Sentinel KQL)
- False positive reduction strategies and tuning notes
- MITRE ATT&CK mapping
- Investigation context and response guidance

## What this is NOT
- Not a lab
- Not a SOC analyst exercise
- Not vendor-rule copy/paste


## How This Is Used (Practical Example)

These detections are designed to be deployed in a SIEM such as Microsoft Sentinel.

Typical usage flow:
1. Deploy base detections (KQL or Sigma) with conservative thresholds.
2. Review early alerts to understand tenant baseline behavior.
3. Apply tuning notes:
   - trusted locations and VPN exclusions
   - threshold adjustments
   - privileged-user scoping
4. Enable correlation detections to raise confidence and severity.
5. Trigger investigation and incident response workflows only on high-signal alerts.

The focus is on reducing alert fatigue and producing actionable security signals rather than high alert volume.
