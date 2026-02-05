# CA004 - Require MFA for Administrators

## Policy Overview

| Attribute | Value |
|-----------|-------|
| **Policy ID** | CA004 |
| **Policy Name** | CA004-Require-MFA-Admins |
| **State** | Report-only |
| **Created** | 02/03/2026 |
| **Last Modified** | 02/03/2026 |

## Purpose

Ensure all privileged administrator accounts always require MFA, regardless of location or other conditions.

## Business Justification

Administrator accounts are high-value targets:
- Have elevated permissions across the tenant
- Can modify security settings
- Can access sensitive data
- Compromise leads to full tenant takeover

Unlike regular users, admins should NEVER bypass MFA, even from trusted locations.

## Configuration

### Assignments

#### Users
| Setting | Value |
|---------|-------|
| Include | Directory roles (see below) |
| Exclude | SG-MFA-Excluded (break glass accounts) |

#### Included Directory Roles
- Global Administrator
- Security Administrator
- User Administrator
- Exchange Administrator
- SharePoint Administrator
- Privileged Role Administrator
- Application Administrator
- Cloud Application Administrator
- Conditional Access Administrator
- Authentication Administrator
- Privileged Authentication Administrator

#### Cloud Apps
| Setting | Value |
|---------|-------|
| Include | All cloud apps |

### Conditions

| Setting | Value |
|---------|-------|
| Configure | Not configured (always apply) |

### Access Controls

#### Grant
| Setting | Value |
|---------|-------|
| Control | Grant access |
| Require | Multifactor authentication |

## Impact Assessment

### Users Affected
- All users with administrative directory roles
- Approximately 2-5% of total users (varies by org)

### Key Difference from CA002
- CA002 excludes trusted locations
- CA004 applies EVERYWHERE — no location exclusions

### Admin Experience
- MFA required on every sign-in
- No exceptions for trusted networks
- Enforces Zero Trust for privileged access

## Testing Results

| Test Date | Mode | Admin Sign-ins | MFA Prompted | Issues/Observations |
|-----------|------|----------------|--------------|--------|
| 02/03/2026 | Report-only | 2 | 2 | Working as expected. Admin accounts always prompted for MFA regardless of location. |

### Test Users
- ✅ Tenant Admin - MFA prompted, sign-in successful
- ✅ Break Glass 1 - Correctly excluded from policy (Global Admin but in exclusion group)

## Rollback Procedure

1. Navigate to Conditional Access policies
2. Open CA004-Require-MFA-Admins
3. Set "Enable policy" to "Off"
4. Click Save
5. Document rollback reason
6. **WARNING:** Disabling exposes admin accounts to increased risk

## Related Documentation

- [Microsoft: Securing privileged access](https://docs.microsoft.com/en-us/azure/active-directory/roles/security-planning)
- [Protect your Microsoft 365 global administrator accounts](https://docs.microsoft.com/en-us/microsoft-365/enterprise/protect-your-global-administrator-accounts)
