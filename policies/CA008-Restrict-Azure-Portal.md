# CA008 - Restrict Azure Portal Access

## Policy Overview

| Attribute | Value |
|-----------|-------|
| **Policy ID** | CA008 |
| **Policy Name** | CA008-Restrict-Azure-Portal |
| **State** | Documented (not deployed) |
| **Created** | 02/03/2026 |
| **Last Modified** | 02/03/2026 |

## Purpose

Prevent non-administrative users from accessing Azure management interfaces, reducing attack surface and preventing accidental misconfigurations.

## Business Justification

Regular users have no business need to access:
- Azure Portal
- Azure PowerShell
- Azure CLI
- Azure Resource Manager APIs

Blocking access:
- Reduces attack surface
- Prevents accidental changes
- Limits reconnaissance by compromised accounts
- Enforces least privilege principle

## Configuration

### Assignments

#### Users
| Setting | Value |
|---------|-------|
| Include | All users |
| Exclude | Directory roles (Global Admin, Security Admin, etc.) |
| Exclude | SG-IT-Operations |
| Exclude | SG-Security-Team |

#### Cloud Apps
| Setting | Value |
|---------|-------|
| Include | Microsoft Azure Management |

### Conditions

| Setting | Value |
|---------|-------|
| Configure | Not configured |

### Access Controls

#### Grant
| Setting | Value |
|---------|-------|
| Control | Block access |

## Implementation Status

| Status | Reason |
|--------|--------|
| **Documented only** | Target application "Microsoft Azure Management" not available in lab environment |

## Intended Behavior

| User Type | Access to Azure Portal |
|-----------|----------------------|
| Global Administrator | ✅ Allowed |
| Security Administrator | ✅ Allowed |
| IT Operations team | ✅ Allowed |
| Security team | ✅ Allowed |
| Regular employees | ❌ Blocked |
| Guests | ❌ Blocked |

## Impact Assessment

### Users Affected
- All non-IT users attempting to access Azure Portal
- Approximately 80-90% of users (business users)

### User Experience
- User navigates to portal.azure.com
- User sees "You cannot access this right now" message
- No access to Azure resources or settings

## Alternative Implementation

If "Microsoft Azure Management" app unavailable, consider:

1. **Azure AD Admin Center restriction** — Block access to Entra admin center
2. **Custom app registration** — Create app targeting Azure management APIs
3. **Azure RBAC** — Remove Reader role from users at subscription level

## Rollback Procedure

1. Navigate to Conditional Access policies
2. Open CA008-Restrict-Azure-Portal
3. Set "Enable policy" to "Off"
4. Click Save
5. Document rollback reason

## Related Documentation

- [Microsoft: Block access to Azure portal](https://docs.microsoft.com/en-us/azure/role-based-access-control/conditional-access-azure-management)
- [Azure management apps](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/concept-conditional-access-cloud-apps#microsoft-azure-management)
