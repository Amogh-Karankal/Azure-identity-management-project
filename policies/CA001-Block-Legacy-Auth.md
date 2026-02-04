# CA001 - Block Legacy Authentication

## Policy Overview

| Attribute | Value |
|-----------|-------|
| **Policy ID** | CA001 |
| **Policy Name** | CA001-Block-Legacy-Authentication |
| **State** | Report-only |
| **Created** | [DATE] |
| **Last Modified** | [DATE] |

## Purpose

Block legacy authentication protocols that don't support modern security features like MFA, protecting against password spray and credential stuffing attacks.

## Business Justification

Legacy authentication protocols (IMAP, POP3, SMTP, older Office clients) are used in over 99% of password spray attacks. These protocols:
- Cannot enforce MFA
- Cannot be protected by Conditional Access
- Are commonly exploited for initial access

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

#### Client Apps
| Setting | Value |
|---------|-------|
| Configure | Yes |
| Browser | Not selected |
| Mobile apps and desktop clients | Not selected |
| Exchange ActiveSync clients | ✅ Selected |
| Other clients | ✅ Selected |

### Access Controls

#### Grant
| Setting | Value |
|---------|-------|
| Control | Block access |

## Impact Assessment

### Users Affected
- Any user or application using legacy authentication protocols
- Old email clients (Outlook 2010, older mobile mail apps)
- Some line-of-business applications using basic auth

### Expected Blocks
- Legacy email clients
- Older mobile email apps
- Scripts using basic authentication

### Mitigation
- Users upgrade to modern authentication clients
- Applications updated to use OAuth/modern auth
- Exceptions handled via exclusion groups if business-critical

## Testing Results

| Test Date | Mode | Sign-ins Evaluated | Would Block | Issues |
|-----------|------|-------------------|-------------|--------|
| [DATE] | Report-only | [NUMBER] | [NUMBER] | [NOTES] |

## Rollback Procedure

1. Navigate to Conditional Access policies
2. Open CA001-Block-Legacy-Authentication
3. Set "Enable policy" to "Off"
4. Click Save
5. Document rollback reason

## Related Documentation

- [Microsoft: Block legacy authentication](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/block-legacy-authentication)
- [NIST SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)
