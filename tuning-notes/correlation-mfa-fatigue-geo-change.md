# Tuning Notes: Correlated MFA Fatigue + Geo Change (Any User)

## Why this detection matters
MFA fatigue alone can be noisy. Geo change alone can be noisy. Correlating the two within a tight window significantly increases confidence of credential compromise.

## Expected false positives
- Corporate VPN egress IP changes
- Mobile networks / roaming behavior
- Legitimate travel
- Helpdesk-driven login troubleshooting

## High-signal indicators (raise severity)
- High failure count (e.g., >=10) before success
- Access to privileged or sensitive applications after the event
- New device sign-in combined with geo change
- Multiple users affected from the same IP ranges (attacker infra)

## Tuning / exclusions
- Exclude trusted named locations and corporate VPN egress ranges
- Consider requiring:
  - success from an IP different than the failures
  - geo change plus new device registration
- Adjust thresholds based on tenant baseline
- Prioritize privileged groups (optional secondary filter)

## Recommended response
1. Contact user to validate MFA prompts and travel/VPN usage.
2. Revoke sessions, reset password, and reset MFA methods if suspicious.
3. Block malicious IPs and enforce Conditional Access (phishing-resistant MFA where possible).
4. Review post-login activity: mailbox rules, OAuth grants, admin actions.
