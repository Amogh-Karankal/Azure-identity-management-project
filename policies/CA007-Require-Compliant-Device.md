# CA007 - Require Compliant Device for Office 365

## Policy Overview

| Attribute | Value |
|-----------|-------|
| **Policy ID** | CA007 |
| **Policy Name** | CA007-Require-Compliant-Device-O365 |
| **State** | Report-only |
| **Created** | 02/03/2026 |
| **Last Modified** | 02/03/2026 |

## Purpose

Ensure corporate data in Office 365 is only accessed from devices that meet organizational security standards through Intune compliance policies.

## Business Justification

Device compliance ensures:
- Devices have required security settings (encryption, PIN)
- Devices are not jailbroken/rooted
- Antivirus is installed and updated
- OS is patched and supported
- Corporate data protected on managed devices

## Configuration

### Assignments

#### Users
| Setting | Value |
|---------|-------|
| Include | All users |
| Exclude | SG-MFA-Excluded, SG-External-Partners |

#### Cloud Apps
| Setting | Value |
|---------|-------|
| Include | Office 365 |

### Conditions

#### Device Platforms
| Setting | Value |
|---------|-------|
| Configure | Yes |
| Include | Windows, macOS |
| Exclude | iOS, Android (handled by app protection policies) |

### Access Controls

#### Grant
| Setting | Value |
|---------|-------|
| Control | Grant access |
| Require | Device to be marked as compliant |
| Multiple controls | Require one of the selected controls |

## Prerequisites

- **Microsoft Intune** enrollment required
- Compliance policies configured in Intune
- Devices enrolled and evaluated

## Device Compliance Requirements (Example)

| Setting | Windows | macOS |
|---------|---------|-------|
| OS Version | Windows 10+ | macOS 12+ |
| Encryption | BitLocker required | FileVault required |
| Antivirus | Microsoft Defender | Required |
| Firewall | Enabled | Enabled |
| Password | Required, 8+ chars | Required |

## Impact Assessment

### Users Affected
- All users accessing Office 365 from Windows/macOS
- Does not affect mobile devices (separate policy)

### Expected Behavior
- Compliant devices: Access granted
- Non-compliant devices: Access blocked
- Unmanaged devices: Access blocked

### Exclusions
- Guest users (SG-External-Partners) — may not have managed devices
- Break glass accounts — emergency access

## Testing Results

| Test Date | Mode | Sign-ins Evaluated | Compliant | Non-Compliant | Issues/Observations |
|-----------|------|-------------------|-----------|---------------|--------|
| 02/03/2026 | Report-only | ~5 | 0 | ~5 | No devices enrolled in Intune. Policy documented for future implementation. |

### Notes
- Intune enrollment required for device compliance evaluation
- Current test environment does not have Intune configured
- All sign-ins from unmanaged devices (expected in lab environment)

### For Production Implementation
1. Enroll devices in Microsoft Intune
2. Configure compliance policies (encryption, PIN, antivirus)
3. Allow 1-2 weeks for devices to report compliance
4. Enable policy after device enrollment complete

### Policy Status
- ✅ Configuration complete
- ⏳ Awaiting Intune enrollment for full testing

## Rollback Procedure

1. Navigate to Conditional Access policies
2. Open CA007-Require-Compliant-Device-O365
3. Set "Enable policy" to "Off"
4. Click Save
5. Document rollback reason

## Related Documentation

- [Microsoft: Require compliant devices](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/howto-conditional-access-policy-compliant-device)
- [Intune device compliance](https://docs.microsoft.com/en-us/mem/intune/protect/device-compliance-get-started)
