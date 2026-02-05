# CA009 - Session Controls for External Users

## Policy Overview

| Attribute | Value |
|-----------|-------|
| **Policy ID** | CA009 |
| **Policy Name** | CA009-Session-Controls-External |
| **State** | Report-only |
| **Created** | 02/03/2026 |
| **Last Modified** | 02/03/2026 |

## Purpose

Apply stricter session controls for guest and external users, requiring MFA and limiting session duration to reduce risk from external identities.

## Business Justification

External users (guests, B2B partners) present additional risk:
- Not under organizational security control
- May use personal/unmanaged devices
- Account security posture unknown
- Should have limited persistent access

Shorter sessions ensure:
- Regular re-verification of identity
- Reduced exposure if account compromised
- Automatic sign-out after period of access

## Configuration

### Assignments

#### Users
| Setting | Value |
|---------|-------|
| Include | Guest or external users |
| Include Types | B2B collaboration guest users |
|  | B2B collaboration member users |
|  | B2B direct connect users |
| Exclude | None |

#### Cloud Apps
| Setting | Value |
|---------|-------|
| Include | All cloud apps |

### Conditions

| Setting | Value |
|---------|-------|
| Configure | Not configured |

### Access Controls

#### Grant
| Setting | Value |
|---------|-------|
| Control | Grant access |
| Require | Multifactor authentication |

#### Session
| Setting | Value |
|---------|-------|
| Sign-in frequency | 4 hours |

## Session Control Explained

| Setting | Value | Effect |
|---------|-------|--------|
| Sign-in frequency | 4 hours | User must re-authenticate every 4 hours |

After 4 hours:
1. User's session token expires
2. User prompted to sign in again
3. MFA required again
4. Access continues after successful authentication

## Impact Assessment

### Users Affected
- All guest users in the tenant
- B2B collaboration partners
- External contractors

### User Experience
- Initial sign-in: MFA required
- Every 4 hours: Re-authentication required
- More prompts than internal users

### Business Consideration
- 4 hours balances security and usability
- Adjust based on partner feedback
- Critical partners may need longer sessions

## Testing Results

| Test Date | Mode | Guest Sign-ins | MFA Prompted | Session Applied | Issues |
|-----------|------|----------------|--------------|-----------------|--------|
| 02/03/2026 | Report-only | 0 | N/A | N/A | No guest users in tenant to test. Policy configuration verified. |

### Notes
- No B2B guest users currently exist in test tenant
- Policy will apply when guest users are invited

### Configuration Verified
- ✅ Target: Guest or external users (B2B collaboration)
- ✅ Grant: Require MFA
- ✅ Session: Sign-in frequency set to 4 hours

### Expected Behavior (When Guests Present)
| Action | Result |
|--------|--------|
| Guest first sign-in | MFA required |
| After 4 hours | Re-authentication required |
| Guest from blocked country | Blocked (CA003 also applies) |

### To Test (Optional)
1. Invite a guest user (personal email)
2. Sign in as guest
3. Verify MFA prompt
4. Wait 4 hours or check sign-in logs for session control

## Rollback Procedure

1. Navigate to Conditional Access policies
2. Open CA009-Session-Controls-External
3. Set "Enable policy" to "Off"
4. Click Save
5. Document rollback reason

## Related Documentation

- [Microsoft: Session lifetime policies](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/howto-conditional-access-session-lifetime)
- [B2B collaboration overview](https://docs.microsoft.com/en-us/azure/active-directory/external-identities/what-is-b2b)
