# Diagrams

This folder contains architecture and flow diagrams for the IAM project.

## Diagram List

| Diagram | Description | Tool Used |
|---------|-------------|-----------|
| architecture-diagram.png | Overall IAM architecture | Draw.io |
| conditional-access-flow.png | CA policy evaluation flow | Draw.io |
| group-structure.png | Security groups and membership | Draw.io |

## How to Create These Diagrams

### Tool: Draw.io (Free)
1. Go to https://app.diagrams.net/
2. Choose "Create New Diagram"
3. Select template or blank
4. Create diagram
5. Export as PNG

### Architecture Diagram - What to Include
```
┌──────────────────────────────────────────────────────────┐
│                    ENTRA ID TENANT                       │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  ┌─────────┐     ┌─────────┐     ┌─────────────────┐     │
│  │  USERS  │────▶│ GROUPS  │────▶│ ADMIN UNITS    │     │
│  │   10    │     │    9    │     │       3         │     │
│  └─────────┘     └─────────┘     └─────────────────┘     │
│                        │                                 │
│                        ▼                                 │
│  ┌──────────────────────────────────────────────────┐    │
│  │           CONDITIONAL ACCESS ENGINE              │    │
│  │                                                  │    │
│  │  • 10 Policies      • Named Locations            │    │
│  │  • MFA Enforcement  • Risk Assessment            │    │
│  │  • Device Compliance • Session Controls          │    │
│  └──────────────────────────────────────────────────┘    │
│                        │                                 │
│                        ▼                                 │
│  ┌──────────────────────────────────────────────────┐    │
│  │              PROTECTED RESOURCES                 │    │
│  │                                                  │    │
│  │    Office 365    Azure Portal    Other Apps      │    │
│  └──────────────────────────────────────────────────┘    │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

### Conditional Access Flow - What to Include
```
               User Sign-in Request
                        │
                        ▼
                ┌───────────────┐
                │ Authentication│
                │   (Password)  │
                └───────┬───────┘
                        │
                        ▼
    ┌───────────────────────────────────────┐
    │       CONDITIONAL ACCESS ENGINE       │
    ├───────────────────────────────────────┤
    │                                       │
    │  Check: User/Group membership         │
    │  Check: Target application            │
    │  Check: Location                      │
    │  Check: Device platform               │
    │  Check: Sign-in risk                  │
    │  Check: User risk                     │
    │                                       │
    └───────────────────┬───────────────────┘
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
    ┌─────────┐   ┌─────────┐   ┌─────────┐
    │  BLOCK  │   │CHALLENGE│   │  GRANT  │
    │         │   │  (MFA)  │   │         │
    └─────────┘   └────┬────┘   └─────────┘
                       │
                       ▼
                ┌─────────────┐
                │  Complete   │
                │    MFA      │
                └──────┬──────┘
                       │
                       ▼
                ┌─────────────┐
                │   ACCESS    │
                │   GRANTED   │
                └─────────────┘
```

### Group Structure - What to Include
```
                ┌─────────────────────┐
                │   ALL EMPLOYEES     │
                │     (Dynamic)       │
                └──────────┬──────────┘
                           │
   ┌───────────────────────┼───────────────────────┐
   │                       │                       │
   ▼                       ▼                       ▼
┌─────────────┐         ┌─────────────┐         ┌─────────────┐
│ IT Security │         │IT Operations│         │  Business   │
│             │         │             │         │             │
│ • Alex      │         │ • Sam       │         │ • Taylor    │
│ • Jordan    │         │ • Casey     │         │ • Morgan    │
└─────────────┘         └─────────────┘         │ • Jamie     │
                                                │ • Riley     │
                                                └─────────────┘
Special Groups:
┌─────────────────┐     ┌─────────────────┐
│  SG-MFA-Excluded│     │   SG-CA-Pilot   │
│                 │     │                 │
│ • BreakGlass1   │     │ • Alex          │
│ • BreakGlass2   │     │ • Jordan        │
└─────────────────┘     │ • Sam           │
                        └─────────────────┘
```
