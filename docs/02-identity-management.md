# Identity Management

## User Management

### User Inventory

| User | UPN | Department | Role | License |
|------|-----|------------|------|---------|
| Alex Security | alex.security@[tenant].onmicrosoft.com | IT Security | Security Analyst | P2 |
| Jordan SecEng | jordan.seceng@[tenant].onmicrosoft.com | IT Security | Security Engineer | P2 |
| Sam ITAdmin | sam.itadmin@[tenant].onmicrosoft.com | IT Operations | System Administrator | P2 |
| Casey HelpDesk | casey.helpdesk@[tenant].onmicrosoft.com | IT Operations | Help Desk Technician | P2 |
| Taylor Finance | taylor.finance@[tenant].onmicrosoft.com | Finance | Finance Manager | P2 |
| Morgan Marketing | morgan.marketing@[tenant].onmicrosoft.com | Marketing | Marketing Specialist | P2 |
| Jamie CEO | jamie.ceo@[tenant].onmicrosoft.com | Executive | Chief Executive Officer | P2 |
| Riley CFO | riley.cfo@[tenant].onmicrosoft.com | Executive | Chief Financial Officer | P2 |
| Break Glass 1 | breakglass1@[tenant].onmicrosoft.com | IT Security | Emergency Access | None |
| Break Glass 2 | breakglass2@[tenant].onmicrosoft.com | IT Security | Emergency Access | None |

### User Provisioning Process

1. Create user account in Entra ID
2. Set temporary password (force change at first login)
3. Assign to appropriate security group(s)
4. Assign to administrative unit
5. Assign P2 license
6. User completes first sign-in and MFA registration

## Group Management

### Security Groups

| Group Name | Type | Members | Purpose |
|------------|------|---------|---------|
| SG-Security-Team | Assigned | Alex, Jordan | IT Security staff |
| SG-IT-Operations | Assigned | Sam, Casey | IT Operations staff |
| SG-Finance | Assigned | Taylor | Finance department |
| SG-Marketing | Assigned | Morgan | Marketing department |
| SG-Executives | Assigned | Jamie, Riley | C-suite executives |
| SG-External-Partners | Assigned | (empty) | Guest users |
| SG-All-Employees | Dynamic | Auto | All active members |
| SG-MFA-Excluded | Assigned | BreakGlass1, BreakGlass2 | CA policy exclusions |
| SG-CA-Pilot | Assigned | Alex, Jordan, Sam | Policy testing |

### Dynamic Group Rules

**SG-All-Employees:**
(user.userType -eq "Member") and (user.accountEnabled -eq true)

### Group Ownership

All groups owned by tenant administrator for this project. In production:
- Department groups → Department managers
- Security groups → Security team
- Executive groups → HR/Executive assistants

## Administrative Units

### AU-IT-Department
- **Members:** Alex, Jordan, Sam, Casey
- **Purpose:** Delegated IT administration
- **Potential delegated roles:** User Administrator, Helpdesk Administrator

### AU-Business-Users
- **Members:** Taylor, Morgan
- **Purpose:** Business user management
- **Potential delegated roles:** User Administrator (limited)

### AU-Executives
- **Members:** Jamie, Riley
- **Purpose:** Sensitive account management
- **Potential delegated roles:** Restricted to Global Admins

## Self-Service Password Reset (SSPR)

### Configuration

| Setting | Value |
|---------|-------|
| Enabled for | SG-All-Employees |
| Methods required | 2 |
| Methods available | Authenticator, Email, Phone, Security Questions |
| Registration required | Yes (at sign-in) |
| Re-confirmation period | 180 days |

### Authentication Methods

1. **Microsoft Authenticator** - Primary
2. **Email** - Secondary
3. **Mobile Phone (SMS)** - Backup
4. **Security Questions** - Additional (5 to register, 3 to reset)

## MFA Configuration

### Enabled Methods

| Method | Status | Target |
|--------|--------|--------|
| Microsoft Authenticator | Enabled | All users |
| SMS | Enabled | All users |
| Email OTP | Enabled | All users |
| FIDO2 Security Keys | Disabled | - |
| Windows Hello | Disabled | - |

### Registration Enforcement

- Registration campaign: Enabled
- Snooze duration: 3 days
- Target: All users except SG-MFA-Excluded
