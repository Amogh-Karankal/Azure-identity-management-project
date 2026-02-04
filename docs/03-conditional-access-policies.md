# Conditional Access Policies

## Policy Overview

| # | Policy Name | State | Target | Grant Control |
|---|-------------|-------|--------|---------------|
| 001 | Block Legacy Authentication | Report-only | All users | Block |
| 002 | Require MFA All Users | Report-only | All users | Require MFA |
| 003 | Block High-Risk Countries | Report-only | All users | Block |
| 004 | Require MFA Admins | Report-only | Admin roles | Require MFA |
| 005 | Require MFA Risky Sign-in | Report-only | All users | Require MFA |
| 006 | Block High-Risk Users | Report-only | All users | Block |
| 007 | Require Compliant Device | Report-only | All users | Require compliance |
| 008 | Restrict Azure Portal | Documented | All users | Block |
| 009 | Session Controls External | Report-only | Guests | MFA + 4hr session |
| 010 | Enhanced Security Executives | Report-only | Executives | MFA + 8hr session |

## Named Locations

### Corporate-Office-Phoenix (Trusted)
- **Type:** IP ranges
- **Trusted:** Yes
- **IP Ranges:** [Your office IP]/32

### Blocked-High-Risk-Countries
- **Type:** Countries
- **Countries:** North Korea, Iran, [others per policy]

### Allowed-Countries
- **Type:** Countries
- **Countries:** United States, [others where employees work]

## Policy Details

### CA001 - Block Legacy Authentication

**Purpose:** Block insecure legacy authentication protocols that don't support MFA.

**Why it matters:** Legacy protocols (IMAP, POP3, SMTP) are used in 99%+ of password spray attacks.

| Assignment | Configuration |
|------------|---------------|
| Users - Include | All users |
| Users - Exclude | SG-MFA-Excluded |
| Cloud apps | All cloud apps |
| Client apps | Exchange ActiveSync, Other clients |
| Grant | Block access |

---

### CA002 - Require MFA for All Users

**Purpose:** Enforce MFA for all users accessing any cloud application.

**Why it matters:** MFA blocks 99.9% of account compromise attacks.

| Assignment | Configuration |
|------------|---------------|
| Users - Include | All users |
| Users - Exclude | SG-MFA-Excluded |
| Cloud apps | All cloud apps |
| Locations - Include | Any location |
| Locations - Exclude | Corporate-Office-Phoenix |
| Grant | Require MFA |

---

### CA003 - Block High-Risk Countries

**Purpose:** Prevent access from geographic regions with high threat activity.

| Assignment | Configuration |
|------------|---------------|
| Users - Include | All users |
| Users - Exclude | SG-MFA-Excluded |
| Cloud apps | All cloud apps |
| Locations - Include | Blocked-High-Risk-Countries |
| Grant | Block access |

---

### CA004 - Require MFA for Administrators

**Purpose:** Ensure privileged accounts always require MFA, even from trusted locations.

| Assignment | Configuration |
|------------|---------------|
| Users - Include | Directory roles (Global Admin, Security Admin, User Admin, etc.) |
| Users - Exclude | SG-MFA-Excluded |
| Cloud apps | All cloud apps |
| Conditions | None (always apply) |
| Grant | Require MFA |

---

### CA005 - Require MFA for Risky Sign-ins

**Purpose:** Automatically require MFA when Azure detects suspicious sign-in behavior.

| Assignment | Configuration |
|------------|---------------|
| Users - Include | All users |
| Users - Exclude | SG-MFA-Excluded |
| Cloud apps | All cloud apps |
| Sign-in risk | High, Medium |
| Grant | Require MFA |

**Requires:** Entra ID P2 license

---

### CA006 - Block High-Risk Users

**Purpose:** Block access for users flagged as likely compromised.

| Assignment | Configuration |
|------------|---------------|
| Users - Include | All users |
| Users - Exclude | SG-MFA-Excluded |
| Cloud apps | All cloud apps |
| User risk | High |
| Grant | Block access |

**Requires:** Entra ID P2 license

---

### CA007 - Require Compliant Device for Office 365

**Purpose:** Ensure corporate data is only accessed from managed devices.

| Assignment | Configuration |
|------------|---------------|
| Users - Include | All users |
| Users - Exclude | SG-MFA-Excluded, SG-External-Partners |
| Cloud apps | Office 365 |
| Device platforms | Windows, macOS |
| Grant | Require compliant device |

**Requires:** Intune enrollment for full enforcement

---

### CA008 - Restrict Azure Portal Access (Documented)

**Purpose:** Prevent non-admin users from accessing Azure management interfaces.

**Status:** Documented only (target app not available in lab)

| Assignment | Configuration |
|------------|---------------|
| Users - Include | All users |
| Users - Exclude | Admin roles, SG-IT-Operations, SG-Security-Team |
| Cloud apps | Microsoft Azure Management |
| Grant | Block access |

---

### CA009 - Session Controls for External Users

**Purpose:** Limit session duration for guest users.

| Assignment | Configuration |
|------------|---------------|
| Users - Include | Guest or external users |
| Users - Exclude | None |
| Cloud apps | All cloud apps |
| Grant | Require MFA |
| Session | Sign-in frequency: 4 hours |

---

### CA010 - Enhanced Security for Executives

**Purpose:** Provide additional protection for high-profile targets.

| Assignment | Configuration |
|------------|---------------|
| Users - Include | SG-Executives |
| Users - Exclude | None |
| Cloud apps | All cloud apps |
| Locations - Include | Any location |
| Locations - Exclude | Corporate-Office-Phoenix |
| Grant | Require MFA |
| Session | Sign-in frequency: 8 hours |

## Policy Rollout Strategy

### Recommended Order (Production)

1. **Week 1:** CA001 (Legacy Auth) - Low user impact
2. **Week 1:** CA003 (Countries) - Usually no impact
3. **Week 2:** CA004 (Admin MFA) - Critical security
4. **Week 2:** CA002 (All Users MFA) - Communicate first!
5. **Week 3:** CA005, CA006 (Risk-based) - Automatic
6. **Week 3:** CA008-010 (Refinements)

### Testing Process

1. Deploy in **Report-only** mode
2. Monitor sign-in logs for 1-2 weeks
3. Review impact in CA Insights
4. Address false positives
5. Enable policy
6. Monitor for issues
