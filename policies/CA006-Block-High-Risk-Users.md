# CA006 - Block High-Risk Users

## Policy Overview

| Attribute | Value |
|-----------|-------|
| **Policy ID** | CA006 |
| **Policy Name** | CA006-Block-High-Risk-Users |
| **State** | Report-only |
| **Created** | 02/03/2026 |
| **Last Modified** | 02/03/2026 |

## Purpose

Block access for users flagged as high-risk by Microsoft Entra ID Protection, indicating likely account compromise.

## Business Justification

When a user account is flagged as high-risk, there's strong evidence of compromise:
- Leaked credentials found on dark web
- User associated with malicious activity
- Account behaving like a bot/automated attack

Blocking immediately contains the breach while investigation occurs.

## Configuration

### Assignments

#### Users
| Setting | Value |
|---------|-------|
| Include | All users |
| Exclude | SG-MFA-Excluded (break glass accounts) |

#### Cloud Apps
| Setting | Value |
|---------|-------|
| Include | All cloud apps |

### Conditions

#### User Risk
| Setting | Value |
|---------|-------|
| Configure | Yes |
| Risk levels | High |

### User Risk vs Sign-in Risk

| Type | Meaning | Example |
|------|---------|---------|
| **User Risk** | Account is likely compromised | Credentials leaked online |
| **Sign-in Risk** | This specific sign-in is suspicious | Anonymous IP, impossible travel |

### Access Controls

#### Grant
| Setting | Value |
|---------|-------|
| Control | Block access |

## Prerequisites

- **Microsoft Entra ID P2 license required**
- Identity Protection must be enabled

## Impact Assessment

### Users Affected
- Users flagged with high user risk
- Typically very few users (compromised accounts)

### What Happens When Blocked
- User cannot sign in to any cloud app
- User sees "Your sign-in was blocked" message
- Admin must investigate and remediate

### Remediation Process
1. Admin reviews user risk in Identity Protection
2. Investigate the risk detection
3. If false positive: Dismiss risk
4. If true positive: Reset password, revoke sessions
5. User risk resets after remediation

## Testing Results

| Test Date | Mode | High-Risk Users | Would Block | Issues/Observations |
|-----------|------|-----------------|-------------|--------|
| 02/03/2026 | Report-only | 0 | 0 | No high-risk users in tenant. Policy configured and ready. |

### Notes
- No user accounts flagged as high-risk during testing period
- User risk is determined by Microsoft Identity Protection based on:
  - Leaked credentials detected on dark web
  - User associated with malicious activity
  - Anomalous user behavior patterns
- Policy will automatically block users when high risk detected

### Verification
- ✅ Policy configuration verified in Conditional Access
- ✅ SG-MFA-Excluded correctly set as exclusion
- ✅ User risk condition set to "High"

## Rollback Procedure

1. Navigate to Conditional Access policies
2. Open CA006-Block-High-Risk-Users
3. Set "Enable policy" to "Off"
4. Click Save
5. Document rollback reason
6. **WARNING:** Disabling allows potentially compromised accounts to access resources

## Related Documentation

- [Microsoft: User risk-based Conditional Access](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/howto-conditional-access-policy-risk-user)
- [Remediate risks and unblock users](https://docs.microsoft.com/en-us/azure/active-directory/identity-protection/howto-identity-protection-remediate-unblock)
