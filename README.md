# Azure Identity & Access Management Project

![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Microsoft Entra ID](https://img.shields.io/badge/Microsoft%20Entra%20ID-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Security](https://img.shields.io/badge/Security-FF6B6B?style=for-the-badge&logo=springsecurity&logoColor=white)

## 🎯 Project Overview

A comprehensive **enterprise identity and access management solution** built on Microsoft Entra ID for a fictional company "Contoso Security Inc." This project demonstrates practical implementation of Zero Trust security principles using Microsoft's identity platform.

### What I Built

- ✅ Microsoft Entra ID tenant configuration from scratch
- ✅ User lifecycle management with groups and administrative units
- ✅ Self-service password reset (SSPR) implementation
- ✅ Multi-factor authentication (MFA) enforcement
- ✅ **10 Conditional Access policies** implementing Zero Trust principles
- ✅ Emergency break glass account procedures

---

## 🏗️ Architecture

![Architecture Diagram](diagrams/architecture-diagram.png)

### Components

| Component | Purpose |
|-----------|---------|
| **Users (10)** | Employees across departments + break glass accounts |
| **Security Groups (9)** | Role-based access control including dynamic groups |
| **Administrative Units (3)** | Delegated administration boundaries |
| **Conditional Access (10)** | Zero Trust policy enforcement |
| **Named Locations (3)** | Geographic-based access control |

---

## 🛡️ Conditional Access Policy Framework

| # | Policy | Purpose | Status |
|---|--------|---------|--------|
| 001 | Block Legacy Authentication | Prevent insecure protocol usage | ✅ Implemented |
| 002 | Require MFA for All Users | Universal MFA enforcement | ✅ Implemented |
| 003 | Block High-Risk Countries | Geographic restrictions | ✅ Implemented |
| 004 | Require MFA for Admins | Enhanced admin protection | ✅ Implemented |
| 005 | Require MFA for Risky Sign-ins | Risk-based authentication | ✅ Implemented |
| 006 | Block High-Risk Users | Compromised account protection | ✅ Implemented |
| 007 | Require Compliant Device | Device trust verification | ✅ Implemented |
| 008 | Restrict Azure Portal | Management plane protection | 📝 Documented |
| 009 | Session Controls for External | Guest user restrictions | ✅ Implemented |
| 010 | Enhanced Security for Executives | VIP protection | ✅ Implemented |

➡️ [View detailed policy documentation](policies/)

---

## 🔐 Security Principles Implemented

### Zero Trust Model
> "Never trust, always verify"

- **Verify explicitly:** Every access request authenticated via MFA
- **Least privilege:** Role-based group membership
- **Assume breach:** Break glass procedures, risk-based policies

### Defense in Depth
```
Layer 1: Identity Verification (MFA)
↓
Layer 2: Device Compliance
↓
Layer 3: Location Restrictions
↓
Layer 4: Risk Assessment
↓
Layer 5: Session Controls

```

## 📊 Technical Implementation

### Identity Structure
```
Contoso Security Inc.
├── IT Department (AU)
│   ├── SG-Security-Team
│   │   ├── Alex Security (Security Analyst)
│   │   └── Jordan SecEng (Security Engineer)
│   └── SG-IT-Operations
│       ├── Sam ITAdmin (System Administrator)
│       └── Casey HelpDesk (Help Desk Technician)
├── Business Users (AU)
│   ├── SG-Finance
│   │   └── Taylor Finance (Finance Manager)
│   └── SG-Marketing
│       └── Morgan Marketing (Marketing Specialist)
└── Executives (AU)
    └── SG-Executives
        ├── Jamie CEO (Chief Executive Officer)
        └── Riley CFO (Chief Financial Officer)
```

### Special Groups

| Group | Type | Purpose |
|-------|------|---------|
| SG-All-Employees | Dynamic | Auto-populates with all members |
| SG-MFA-Excluded | Assigned | Break glass accounts (CA exclusion) |
| SG-CA-Pilot | Assigned | Policy testing before rollout |

---

## 🧪 Testing & Validation

### Test Results

| User | Expected | Result |
|------|----------|--------|
| Alex Security | MFA prompted | ✅ Pass |
| Sam ITAdmin | MFA prompted | ✅ Pass |
| Jamie CEO | MFA + session controls | ✅ Pass |
| Break Glass 1 | No MFA (can skip) | ✅ Pass |

### Sign-in Log Analysis

Successfully verified:
- CA policies evaluate correctly
- MFA enforcement working
- Break glass exclusions functional
- Session controls applied to executives

---

## 📁 Documentation

| Document | Description |
|----------|-------------|
| [Architecture Overview](docs/01-architecture-overview.md) | System design and components |
| [Identity Management](docs/02-identity-management.md) | Users, groups, admin units |
| [Conditional Access Policies](docs/03-conditional-access-policies.md) | All 10 policies detailed |
| [Break Glass Procedures](docs/04-break-glass-procedures.md) | Emergency access protocols |
| [Lessons Learned](docs/05-lessons-learned.md) | Key insights and takeaways |

---

## 🛠️ Technologies Used

- **Microsoft Entra ID** (formerly Azure AD)
- **Conditional Access**
- **Identity Protection**
- **Multi-Factor Authentication**
- **Self-Service Password Reset**
- **Administrative Units**
- **Dynamic Groups**

---

## 📜 Certifications Demonstrated

This project demonstrates practical skills for:

| Certification | Skills Covered |
|---------------|----------------|
| **SC-300** | Identity and Access Administrator |
| **SC-100** | Cybersecurity Architect Expert |
| **AZ-900** | Azure Fundamentals |

---

## 🚀 Key Achievements

1. **Implemented Zero Trust architecture** using Microsoft's identity platform
2. **Created 10 Conditional Access policies** covering major security scenarios
3. **Designed break glass procedures** for emergency access
4. **Configured risk-based authentication** for adaptive security
5. **Built scalable group structure** with dynamic membership

---

## 📈 Future Enhancements

- [ ] Privileged Identity Management (PIM) for just-in-time access
- [ ] Microsoft Sentinel integration for SIEM
- [ ] Access Reviews for periodic certification
- [ ] Entitlement Management for access packages

---

## 👤 Author

**Amogh Karankal**

- 📧 Email: amogh.karankal@gmail.com
- 💼 LinkedIn: [linkedin.com/in/amoghkarankal](https://linkedin.com/in/amoghkarankal)
- 🐙 GitHub: [github.com/Amogh-Karankal](https://github.com/Amogh-Karankal)

---

## 📄 License

This project is for educational and portfolio purposes.
