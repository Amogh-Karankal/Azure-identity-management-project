# Lessons Learned

## Technical Insights

### 1. Sign-in Logs Terminology is Confusing

**Discovery:** In sign-in logs, Conditional Access "Failure" doesn't mean the sign-in failed.

**What it actually means:**
| Term | Actual Meaning |
|------|----------------|
| CA: Failure | User was challenged (MFA prompted) |
| CA: Success | User met requirements upfront |
| CA: Not Applied | Policy didn't apply or already authenticated |

**Key insight:** "CA Failure" + "Status Success" = Policy worked correctly!

### 2. Report-Only Mode is Essential

**Best Practice:** Always deploy CA policies in report-only first.

**Why:**
- See impact before enforcement
- Identify unexpected blocks
- Find users who would be affected
- Adjust policies safely

**Recommended timeline:** 1-2 weeks in report-only before enabling

### 3. Break Glass Accounts Need Special Care

**Critical requirements:**
- Must be excluded from ALL CA policies
- Must NOT have MFA enrolled
- Must have strong, unique passwords
- Must be monitored for usage

**Testing insight:** Break glass accounts should show "Skip" option for MFA, not forced enrollment.

### 4. Dynamic Groups Have Delays

**Observation:** Dynamic group membership can take up to 24 hours to fully populate.

**Implication:** Don't rely on dynamic groups for immediate access changes.

### 5. License Management Moved to M365 Admin Center

**2026 Change:** Entra ID no longer manages licenses directly.

**New process:**
1. Create admin user in tenant
2. Sign into admin.microsoft.com with tenant account
3. Manage licenses under Billing → Purchase services

### 6. Policy Order Matters

**Discovery:** Policies are evaluated together, but some take precedence.

**Block > Grant:** If any policy blocks, access is denied regardless of other policies.

### 7. Sign-in Logs Have Delays

**Observation:** Sign-in events can take 5-30 minutes to appear in logs.

**Tip:** Be patient when testing; refresh logs periodically.

## Best Practices Identified

### Identity Management

1. **Every group needs an owner** - Critical for governance
2. **Use consistent naming conventions** - SG- for security groups, AU- for admin units
3. **Document everything** - Future troubleshooting depends on it
4. **Assign minimum necessary licenses** - Break glass accounts need none

### Conditional Access

1. **Start with report-only** - Always test before enforcing
2. **Block legacy auth first** - Low impact, high security value
3. **Create exclusion groups** - Easier than excluding individual users
4. **Layer your defenses** - MFA + location + risk + device

### Operations

1. **Test break glass quarterly** - Ensure emergency access works
2. **Monitor sign-in logs** - Detect anomalies early
3. **Review policies regularly** - Requirements change over time
4. **Document changes** - Audit trail is essential

## Challenges Encountered

### Challenge 1: M365 Developer Program Not Available
**Problem:** Couldn't get sandbox subscription
**Solution:** Used Azure Free Account + P2 Trial

### Challenge 2: Azure Portal App Not Found
**Problem:** Couldn't find "Microsoft Azure Management" for CA008
**Solution:** Documented policy theoretically; noted as lab limitation

### Challenge 3: "Unknown Future Value" in Logs
**Problem:** CA policy results showed garbled text
**Solution:** Portal bug; verified policies working via actual MFA prompts

## Skills Demonstrated

| Skill | Evidence |
|-------|----------|
| Identity architecture design | Built complete IAM structure |
| Conditional Access configuration | Created 10 policies |
| Zero Trust implementation | Layered security controls |
| Security operations | Break glass procedures, monitoring |
| Documentation | Comprehensive technical docs |
| Troubleshooting | Resolved portal issues, log analysis |

## Recommendations for Future Projects

1. **Add Privileged Identity Management** - Just-in-time access for admins
2. **Integrate Microsoft Sentinel** - SIEM for security monitoring
3. **Implement Access Reviews** - Periodic access certification
4. **Add Application Proxy** - Secure on-premises app access
5. **Configure Entitlement Management** - Self-service access packages
