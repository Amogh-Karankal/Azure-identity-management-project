# CA003 - Block High-Risk Countries

## Policy Overview

| Attribute | Value |
|-----------|-------|
| **Policy ID** | CA003 |
| **Policy Name** | CA003-Block-High-Risk-Countries |
| **State** | Report-only |
| **Created** | 02/03/2026 |
| **Last Modified** | 02/03/2026 |

## Purpose

Prevent access from geographic regions with high threat activity where the organization has no legitimate business presence.

## Business Justification

Geographic-based blocking reduces attack surface by:
- Eliminating access from known threat actor regions
- Reducing noise in security logs
- Blocking opportunistic attacks from specific countries
- Supporting compliance with data sovereignty requirements

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
| Include | Blocked-High-Risk-Countries |

### Named Location: Blocked-High-Risk-Countries
| Setting | Value |
|---------|-------|
| Type | Countries |
| Countries | North Korea, Iran, [others per policy] |

### Access Controls

#### Grant
| Setting | Value |
|---------|-------|
| Control | Block access |

## Impact Assessment

### Users Affected
- Users attempting to sign in from blocked countries
- Users traveling to blocked regions
- VPN users with exit nodes in blocked countries

### Legitimate Access Scenarios
- Employee travel to blocked region (temporary exclusion needed)
- VPN with foreign exit node (user should change VPN server)

### Mitigation
- Temporary exclusion group for travelers
- Clear communication about blocked regions
- VPN guidance for users

## Testing Results

| Test Date | Mode | Sign-ins Evaluated | Would Block | Issues/Observations |
|-----------|------|-------------------|-------------|--------|
| 2026-02-05 | Report-only | ~5 | 0 | No sign-ins from blocked countries detected. Policy ready for enforcement. |

### Notes
- All test sign-ins originated from United States
- Policy would block if sign-in attempted from North Korea, Iran, or other blocked regions
- Cannot easily test without VPN to blocked country

## Rollback Procedure

1. Navigate to Conditional Access policies
2. Open CA003-Block-High-Risk-Countries
3. Set "Enable policy" to "Off"
4. Click Save
5. Document rollback reason

## Related Documentation

- [Microsoft: Location conditions](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/location-condition)
- [Named locations configuration](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/location-condition#named-locations)
