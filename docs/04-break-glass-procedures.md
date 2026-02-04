# Break Glass Account Emergency Procedures

## Purpose

Break glass accounts provide emergency access to Microsoft Entra ID when:
- Azure MFA service is experiencing an outage
- Conditional Access policies block all admin access
- The last admin account is locked out
- Critical system recovery is needed

## Account Inventory

| Account | UPN | Role | MFA Status |
|---------|-----|------|------------|
| Break Glass 1 | breakglass1@[tenant].onmicrosoft.com | Global Administrator | Not enrolled |
| Break Glass 2 | breakglass2@[tenant].onmicrosoft.com | Global Administrator | Not enrolled |

## Security Configuration

### What Makes These Accounts Special

| Setting | Configuration | Reason |
|---------|---------------|--------|
| MFA | Not enrolled | Must work when MFA is down |
| CA Policies | Excluded (SG-MFA-Excluded) | Must bypass all policies |
| Licenses | None assigned | Reduce attack surface |
| Role | Global Administrator | Full access for recovery |
| Password | 20+ characters, random | Maximum security |

### Password Requirements

- **Length:** Minimum 20 characters
- **Complexity:** Uppercase, lowercase, numbers, special characters
- **Generation:** Randomly generated (not memorable)
- **Storage:** Physical secure location or approved vault
- **Rotation:** After any use

## Access Procedure

### When to Use

✅ **APPROPRIATE USE:**
- Azure MFA service is down globally
- All admin accounts are locked out
- Conditional Access blocking all admin access
- Disaster recovery scenarios

❌ **NEVER USE FOR:**
- Convenience
- Bypassing MFA for testing
- Daily administrative tasks
- Sharing with others

### Step-by-Step Access

1. **Verify emergency conditions exist**
   - Confirm MFA/CA outage from Azure Status page
   - Document the issue

2. **Retrieve credentials**
   - Access secure storage (requires two people if possible)
   - Retrieve password for breakglass1 or breakglass2

3. **Sign in**
   - Use InPrivate/Incognito browser
   - Go to https://portal.azure.com
   - Sign in with break glass account
   - Skip MFA registration if prompted

4. **Perform emergency actions only**
   - Fix the immediate issue
   - Do not perform unrelated tasks
   - Document all actions taken

5. **Sign out immediately**
   - Close all browser windows
   - Clear browser cache

## Post-Use Procedures (MANDATORY)

Complete these steps within 24 hours of any break glass usage:

### 1. Change Password
- Generate new random password
- Update secure storage
- Test new password works

### 2. Document Usage
**Template:**
| Field | Details |
|-------|---------|
| Date/Time | _______________ |
| Account Used | _______________ |
| Reason | _______________ |
| Actions Taken | _______________ |
| Personnel Involved | _______________ |

### 3. Review Audit Logs
- Check for any unauthorized access
- Verify only expected actions were taken
- Export logs for records

### 4. Notify Security Team
- Email security distribution list
- Include usage documentation
- Schedule incident review

### 5. Incident Review
- Conduct within 24-48 hours
- Identify root cause
- Implement preventive measures

## Monitoring Requirements

### Alerts to Configure

| Alert | Trigger | Action |
|-------|---------|--------|
| Break glass sign-in | Any sign-in by breakglass1 or breakglass2 | Immediate notification |
| Password change | Password modified on break glass account | Investigate immediately |
| Role change | Any role modification | Investigate immediately |

### Regular Reviews

| Review | Frequency | Owner |
|--------|-----------|-------|
| Audit log review | Weekly | Security Team |
| Password rotation | Quarterly (or after use) | Security Team |
| Access verification | Quarterly | Security Team |
| Procedure review | Annually | Security Team |

## Testing Schedule

Test break glass procedures quarterly:

1. **Verify credentials work** (sign in, then sign out)
2. **Verify CA exclusions** (MFA should be skippable)
3. **Verify alerting works** (check notification received)
4. **Update documentation** as needed

## Emergency Contacts

| Role | Contact | Phone |
|------|---------|-------|
| Primary Admin | [Name] | [Phone] |
| Backup Admin | [Name] | [Phone] |
| Microsoft Support | N/A | 1-800-Microsoft |
