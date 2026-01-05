# Tuning Notes: MFA Fatigue (Failures Spike then Success)

## Why this detection matters
Attackers may trigger repeated MFA prompts (push spamming) until a user approves one, resulting in account takeover.

## Expected false positives
- Users mistyping passwords repeatedly then succeeding
- MFA delivery issues causing retries
- Helpdesk troubleshooting sessions
- Noisy apps during SSO configuration changes

## High-signal indicators (raise severity)
- Success from a new IP, new device, or new geo
- Correlated impossible travel or risky sign-in indicators
- Access to admin portals or sensitive apps immediately after success
- Multiple users showing similar patterns from same IP range (automation/attacker infra)

## Tuning / exclusions
- Require success from a different IP/geo than the failures (higher fidelity)
- Exclude trusted locations and corporate VPN egress IPs
- Tune threshold (failures >= 5) based on your tenant baseline
- Focus on privileged users / admin roles for higher priority

## Recommended triage workflow
1. Validate user: did they receive repeated MFA prompts?
2. Review sign-in context: IP, device, geo, client app, target apps.
3. If suspicious: revoke sessions, reset password, reset MFA methods, block IP / enforce CA policy.
4. Perform follow-up: check mailbox rules, OAuth grants, and recent admin actions.
