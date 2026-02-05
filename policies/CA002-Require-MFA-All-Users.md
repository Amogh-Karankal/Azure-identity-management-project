# CA002 - Require MFA for All Users

## Policy Overview

| Attribute | Value |
|-----------|-------|
| **Policy ID** | CA002 |
| **Policy Name** | CA002-Require-MFA-All-Users |
| **State** | Report-only |
| **Created** | 02/03/2026 |
| **Last Modified** | 02/03/2026 |

## Purpose

Enforce multi-factor authentication for all users accessing any cloud application, providing a baseline security layer across the organization.

## Business Justification

MFA blocks 99.9% of account compromise attacks. By requiring a second form of verification, even compromised passwords cannot be used to gain unauthorized access.

Key benefits:
- Prevents credential theft attacks
- Protects against phishing
- Meets compliance requirements
- Industry best practice

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

#### Locations
| Setting | Value |
|---------|-------|
| Configure | Yes |
| Include | Any location |
| Exclude | Corporate-Office-Phoenix (trusted) |

### Access Controls

#### Grant
| Setting | Value |
|---------|-------|
| Control | Grant access |
| Require | Multifactor authentication |

## Impact Assessment

### Users Affected
- All users signing in from outside trusted locations
- Remote workers
- Users on personal devices

### Expected Behavior
- Users prompted for MFA on first sign-in
- MFA remembered based on token lifetime
- Trusted location users bypass MFA

### User Communication Required
- Announce MFA rollout 2 weeks before enabling
- Provide MFA registration instructions
- Share help desk contact for issues

## Testing Results

| Test Date | Mode | Sign-ins Evaluated | MFA Prompted | Issues/Observations |
|-----------|------|-------------------|--------------|--------|
| 02/03/2026 | Report-only | ~5 | 3 | MFA enforced successfully. Break glass account excluded as expected. |

### Test Users
- ✅ Alex Security - MFA prompted, sign-in successful
- ✅ Sam ITAdmin - MFA prompted, sign-in successful  
- ✅ Break Glass 1 - MFA skippable, sign-in successful (correctly excluded)

## Rollback Procedure

1. Navigate to Conditional Access policies
2. Open CA002-Require-MFA-All-Users
3. Set "Enable policy" to "Off"
4. Click Save
5. Document rollback reason
6. Communicate to users if needed

## Related Documentation

- [Microsoft: Require MFA for all users](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/howto-conditional-access-policy-all-users-mfa)
- [MFA deployment guide](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-mfa-getstarted)
