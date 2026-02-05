# CA010 - Enhanced Security for Executives

## Policy Overview

| Attribute | Value |
|-----------|-------|
| **Policy ID** | CA010 |
| **Policy Name** | CA010-Enhanced-Security-Executives |
| **State** | Report-only |
| **Created** | 02/03/2026 |
| **Last Modified** | 02/03/2026 |

## Purpose

Provide additional protection for high-profile executive users who are frequent targets of sophisticated attacks like whaling and business email compromise.

## Business Justification

Executives face elevated threats:
- **Whaling attacks** — Targeted phishing at C-suite
- **Business Email Compromise (BEC)** — Impersonation for fraud
- **Credential theft** — High-value target for attackers
- **Data exfiltration** — Access to sensitive strategic info

Enhanced controls:
- MFA everywhere (no trusted location bypass)
- Shorter session lifetime
- More frequent re-authentication

## Configuration

### Assignments

#### Users
| Setting | Value |
|---------|-------|
| Include | SG-Executives |
| Exclude | None (executives don't get exclusions) |

#### Group Members: SG-Executives
- Jamie CEO (Chief Executive Officer)
- Riley CFO (Chief Financial Officer)

#### Cloud Apps
| Setting | Value |
|---------|-------|
| Include | All cloud apps |

### Conditions

#### Locations
| Setting | Value |
|---------|-------|
| Configure | Yes |
| Include | Any location |
| Exclude | Corporate-Office-Phoenix |

### Access Controls

#### Grant
| Setting | Value |
|---------|-------|
| Control | Grant access |
| Require | Multifactor authentication |
| Multiple controls | Require all selected controls |

#### Session
| Setting | Value |
|---------|-------|
| Sign-in frequency | 8 hours |

## Policy Comparison: Executives vs Regular Users

| Control | Regular Users (CA002) | Executives (CA010) |
|---------|----------------------|-------------------|
| MFA required | Yes (outside office) | Yes (outside office) |
| Trusted location bypass | Yes | Yes |
| Session lifetime | Default (browser) | 8 hours max |
| Re-authentication | When token expires | Every 8 hours |

## Why 8-Hour Session?

- Matches typical workday
- Forces daily re-authentication when remote
- Limits exposure window if compromised
- Balances security with usability

## Impact Assessment

### Users Affected
- Members of SG-Executives group
- Currently: Jamie CEO, Riley CFO
- Approximately 2-5 users in typical org

### User Experience
- MFA on every sign-in from outside office
- Must re-authenticate after 8 hours
- More secure but slightly more friction

### Executive Communication
- Brief executives on enhanced security
- Explain business justification
- Provide dedicated support contact

## Testing Results

| Test Date | Mode | Executive Sign-ins | MFA Prompted | Session Applied | Issues |
|-----------|------|-------------------|--------------|-----------------|--------|
| 02/03/2026 | Report-only | 1 | 1 | Yes (8 hours) | Working as expected. Executive user prompted for MFA with session controls. |

### Test Users
- ✅ Jamie CEO - MFA prompted, 8-hour session applied, sign-in successful

### Verification Steps
1. Signed in as jamie.ceo@[tenant].onmicrosoft.com
2. MFA prompt appeared (completed successfully)
3. Checked sign-in logs → CA010 policy applied
4. Session control showing 8-hour sign-in frequency

### Sign-in Log Details
| Field | Value |
|-------|-------|
| User | Jamie CEO |
| Policy Applied | CA010-Enhanced-Security-Executives |
| Grant Control | MFA - Satisfied |
| Session Control | Sign-in frequency: 8 hours |

### Notes
- Executives do not bypass MFA even from trusted locations (by design)
- 8-hour session ensures daily re-authentication for remote work
- Policy provides additional protection for high-value targets

## Rollback Procedure

1. Navigate to Conditional Access policies
2. Open CA010-Enhanced-Security-Executives
3. Set "Enable policy" to "Off"
4. Click Save
5. Document rollback reason
6. **WARNING:** Executives will have reduced protection

## Future Enhancements

Consider adding:
- **Phishing-resistant MFA** — FIDO2 keys for executives
- **Privileged Identity Management** — Just-in-time access
- **Stricter device requirements** — Corporate device only
- **Impossible travel alerts** — Immediate notification

## Related Documentation

- [Microsoft: Protecting privileged users](https://docs.microsoft.com/en-us/azure/active-directory/roles/security-planning)
- [Business email compromise protection](https://docs.microsoft.com/en-us/microsoft-365/security/office-365-security/anti-phishing-protection)
