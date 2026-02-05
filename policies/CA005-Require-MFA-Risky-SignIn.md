# CA005 - Require MFA for Risky Sign-ins

## Policy Overview

| Attribute | Value |
|-----------|-------|
| **Policy ID** | CA005 |
| **Policy Name** | CA005-Require-MFA-Risky-SignIn |
| **State** | Report-only |
| **Created** | 02/03/2026 |
| **Last Modified** | 02/03/2026 |

## Purpose

Automatically require MFA when Microsoft Entra ID Protection detects suspicious sign-in behavior, providing adaptive security based on real-time risk assessment.

## Business Justification

Risk-based authentication provides:
- Adaptive security that responds to threats
- Better user experience (no MFA when risk is low)
- Protection against sophisticated attacks
- Leverages Microsoft's threat intelligence

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

#### Sign-in Risk
| Setting | Value |
|---------|-------|
| Configure | Yes |
| Risk levels | High, Medium |

### Sign-in Risk Levels Explained

| Level | Examples |
|-------|----------|
| **High** | Sign-in from anonymous IP, impossible travel, malware-linked IP |
| **Medium** | Unfamiliar sign-in properties, atypical travel |
| **Low** | Minor anomalies |

### Access Controls

#### Grant
| Setting | Value |
|---------|-------|
| Control | Grant access |
| Require | Multifactor authentication |

## Prerequisites

- **Microsoft Entra ID P2 license required**
- Identity Protection must be enabled

## Impact Assessment

### Users Affected
- Users with detected risky sign-in behavior
- Typically a small percentage of sign-ins

### Scenarios That Trigger MFA
- Signing in from new country
- Using anonymous IP (Tor, VPN)
- Impossible travel detected
- Sign-in from infected device

### User Experience
- Normal sign-ins: No additional MFA (if CA002 excluded location applies)
- Risky sign-ins: MFA prompted automatically

## Testing Results

| Test Date | Mode | Sign-ins Evaluated | Risk Detected | MFA Prompted | Issues/Observations |
|-----------|------|-------------------|---------------|--------------|--------|
| 02/03/2026 | Report-only | ~5 | 0 | 0 | No risky sign-ins detected during testing. Policy configured correctly. |

### Notes
- All test sign-ins were from known locations with no risk indicators
- Risk-based policies trigger automatically when Microsoft detects anomalies
- Cannot easily simulate risky sign-in without VPN/Tor or impossible travel
- Policy will activate when medium or high sign-in risk detected

### Risk Levels Configured
- ✅ High risk - Will require MFA
- ✅ Medium risk - Will require MFA
- ☐ Low risk - Not configured (by design)

## Rollback Procedure

1. Navigate to Conditional Access policies
2. Open CA005-Require-MFA-Risky-SignIn
3. Set "Enable policy" to "Off"
4. Click Save
5. Document rollback reason

## Related Documentation

- [Microsoft: Sign-in risk-based Conditional Access](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/howto-conditional-access-policy-risk)
- [What is Identity Protection?](https://docs.microsoft.com/en-us/azure/active-directory/identity-protection/overview-identity-protection)
