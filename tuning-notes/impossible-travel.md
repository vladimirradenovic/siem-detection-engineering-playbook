# Tuning Notes: Impossible Travel / High Geo-Velocity Sign-ins

## Why this detection matters
Impossible travel patterns often indicate compromised credentials, session hijack, token replay, or shared accounts.

## Expected false positives
- Corporate VPN egress IP changes (same user appears in multiple countries)
- Mobile carrier routing changes
- Frequent travelers / remote workforce
- Split tunneling or browser privacy networks

## High-signal indicators (raise severity)
- Impossible travel followed by MFA failures or unusual MFA prompts
- New device + new location + unusual application access
- Sign-ins to admin portals (Azure Portal, M365 Admin) shortly after the travel event
- Multiple accounts showing similar geo patterns (possible proxy infrastructure)

## Tuning / exclusions
- Exclude trusted locations / corporate VPN egress IP ranges
- Focus on successful sign-ins (or successful after multiple failures)
- Apply thresholds (e.g., multiple geo changes within 2 hours)
- Enrich with Conditional Access outcomes if available (MFA required/failed)

## Recommended triage workflow
1. Confirm user context: expected travel, VPN use, role/privilege.
2. Review sign-in details: IP reputation, device, client app, target apps.
3. Check for related anomalies: impossible travel across multiple services, new device registration, mailbox access patterns.
4. If suspicious:
   - force password reset and revoke sessions
   - review MFA methods and reset if needed
   - block IP / add Conditional Access restrictions
   - assess for lateral movement indicators

## Severity suggestion
- Medium by default
- High if correlated with new device / privileged apps / MFA anomalies
- Critical if confirmed compromise indicators exist
