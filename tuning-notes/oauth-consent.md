# Tuning Notes: Suspicious OAuth Consent / Permission Grants

## Why this detection matters
OAuth consent and permission grants can be abused to obtain persistent access (token theft / malicious app registration), especially when high-privilege scopes are granted or admin consent is used unexpectedly.

## Expected false positives
- Legitimate new SaaS integrations (e.g., Jira, Slack, Zoom, CRM tools) during onboarding
- Approved internal applications requesting additional scopes
- Admins granting consent as part of normal app governance
- Security tooling integrations that periodically renew permissions

## High-signal indicators (raise severity)
- Admin consent performed by an unusual admin account or outside business hours
- Newly created app/service principal followed by consent or role assignment
- Consent granting high-privilege scopes (e.g., Mail.Read, Mail.ReadWrite, offline_access, Directory.Read.All, User.Read.All)
- Multiple consents in a short time window from the same initiator
- Consent activity followed by anomalous sign-ins (new geo, new device, impossible travel)

## Tuning / exclusions (reduce noise)
- Maintain an allowlist of approved enterprise apps and known service principals
- Exclude known administrative break-glass or automation accounts after validation
- Apply thresholds (e.g., alert only if >N consents in 1h) for noisy tenants
- Restrict to admin-consent events or high-privilege scopes for higher fidelity

## Recommended triage workflow
1. Identify the initiating user/account and confirm if they are an expected admin.
2. Review the target application/service principal:
   - creation time
   - publisher verification / tenant origin
   - requested scopes/roles
3. Confirm whether the app is approved by IT/security.
4. Check for related suspicious sign-ins for the initiator and app:
   - unusual location/device
   - spikes in authentication failures
5. If suspicious:
   - revoke consent / remove OAuth grants
   - disable or delete the service principal
   - reset credentials for compromised accounts
   - review mailbox access and audit logs

## Severity suggestion
- Medium by default
- High if admin consent is unusual or high-privilege scopes are granted
- Critical if correlated with confirmed compromise indicators
