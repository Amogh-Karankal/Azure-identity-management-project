# Architecture Overview

## Introduction

This document describes the identity and access management architecture implemented for Contoso Security Inc. using Microsoft Entra ID.

## Design Principles

### 1. Zero Trust
Every access request is fully authenticated, authorized, and encrypted before granting access.

### 2. Least Privilege
Users receive minimum permissions necessary to perform their job functions.

### 3. Defense in Depth
Multiple layers of security controls protect organizational resources.

### 4. Assume Breach
Security controls designed assuming attackers may already have access.

## Architecture Components

### Identity Provider
- **Microsoft Entra ID** serves as the central identity provider
- All authentication flows through Entra ID
- MFA enforced via Conditional Access

### User Structure
```
Total Users: 10
├── Regular Employees: 8
│   ├── IT Security: 2
│   ├── IT Operations: 2
│   ├── Finance: 1
│   ├── Marketing: 1
│   └── Executives: 2
└── Emergency Accounts: 2
└── Break Glass: 2
```

### Group Structure
```
Total Groups: 9
├── Department Groups: 6 (Assigned membership)
├── Dynamic Groups: 1 (Auto-populated)
├── Exclusion Groups: 1 (Break glass)
└── Pilot Groups: 1 (Testing)
```

### Administrative Boundaries
```
Administrative Units: 3
├── AU-IT-Department (4 users)
├── AU-Business-Users (2 users)
└── AU-Executives (2 users)
```

## Security Layers

### Layer 1: Authentication
- Primary: Password
- Secondary: Microsoft Authenticator (MFA)
- Methods: Push notification, TOTP, SMS (backup)

### Layer 2: Conditional Access
- 10 policies enforcing various security requirements
- Risk-based authentication
- Location-based restrictions

### Layer 3: Session Management
- Token lifetime controls
- Sign-in frequency enforcement
- Persistent session restrictions

## Data Flow
```
User Request
│
▼
┌─────────────────┐
│  Entra ID       │
│  Authentication │
└────────┬────────┘
│
▼
┌─────────────────┐
│  Conditional    │──── Risk Assessment
│  Access Engine  │──── Location Check
└────────┬────────┘──── Device Compliance
│
▼
┌─────────────────┐
│  Grant/Block    │
│  Decision       │
└────────┬────────┘
│
┌────┴────┐
▼         ▼
Access    Challenge
Granted   (MFA/Block)
```

## High Availability Considerations

### Break Glass Accounts
- 2 emergency access accounts
- Excluded from all CA policies
- No MFA requirement
- Passwords stored securely offline
- Global Administrator role assigned

### Monitoring
- Sign-in logs retention
- Audit log tracking
- Alert configuration for break glass usage

## Compliance Alignment

This architecture supports:
- **NIST 800-63B** - Digital Identity Guidelines
- **CIS Controls** - Identity and Access Management
- **Zero Trust Maturity Model** - Identity pillar
