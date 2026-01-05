# Tuning Notes: Correlated MFA Fatigue + Success (Privileged Users)

## Why this detection matters
MFA fatigue is noisy for general users. When the same pattern occurs for privileged accounts and ends in success, the likelihood of compromise increases significantly.

## Privileged scope options (production)
- Microsoft Sentinel watchlist of admin UPNs
- IdentityInfo table enrichment (if available)
- Entra ID roles/groups mapping (Global Admin, Security Admin, etc.)

## Expected false positives
- Admins repeatedly mistyping passwords then succeeding
- MFA delivery problems causing retries
- Admins testing Conditional Access policies

## High-signal indicators (raise severity)
- Success from new device or unusual client app
- Success from unfamiliar IP range or unusual geo for that admin
- Immediate access to sensitive apps (Azure Portal, M365 Admin, IAM tools)
- Repeated patterns across multiple privileged accounts from similar IP ranges

## Tuning / exclusions
- Exclude corporate VPN egress IPs and trusted locations
- Require success from different IP/geo than failures for higher fidelity
- Increase threshold for noisy environments (e.g., failures >= 7)
- Prioritize only high-privileged roles if the admin list is broad

## Recommended response
1. Contact the admin immediately (verify if prompts were expected).
2. Revoke sessions + reset password.
3. Reset MFA methods and enforce phishing-resistant MFA if applicable.
4. Review recent admin actions and sign-in history for lateral movement indicators.
