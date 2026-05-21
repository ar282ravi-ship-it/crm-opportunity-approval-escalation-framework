# CRM Opportunity Approval Escalation Framework

A Dynamics 365 CRM + Power Automate solution for automating managerial approval processes with reminder and escalation handling.

---

## Overview

This project automates approval workflows for high-value opportunities inside Dynamics 365 CRM.

The framework:

- Sends approval requests to managers
- Tracks approval status
- Sends reminder notifications
- Escalates approvals to senior manager
- Updates CRM records automatically

---

## Business Problem

In enterprise sales environments, approval delays can slow opportunity progression and impact revenue.

Managers may ignore approval requests, forcing sales teams to manually follow up.

This solution addresses the problem using Power Automate-based approval escalation.

---

## Features

### Automated Approval Creation
Creates approval requests for managers.

### Reminder Automation
Sends reminders every 24 hours when no response is received.

### Escalation Logic
Escalates approval to senior manager after reminder threshold.

### CRM Status Tracking
Automatically updates approval status:

- Approved
- Rejected
- Escalated

### Configurable Thresholds

Approval triggers based on:

```text
Estimated Revenue > 500000
OR
Discount Percentage > 15
```

---

## Solution Architecture

```text
Opportunity Updated
        |
        v
Threshold Validation
        |
        v
Manager Approval
        |
     +--+--+
     |     |
     v     v
Approve Ignore
   |        |
   v        v
Approved  Reminder Loop
              |
              v
     Reminder Count >= 2
              |
              v
     Senior Manager Approval
```

---

## Technology Stack

- Dynamics 365 CRM
- Power Automate
- Approval Connector
- Outlook Connector

---

## Project Structure

```text
crm-opportunity-approval-escalation-framework/
│
├── solution/
│   └── CRMOpportunityApprovalFramework_1_0_0_1.zip
│
├── screenshots/
│
├── docs/
│   ├── business-scenario.md
│   ├── setup-guide.md
│   ├── architecture.md
│   └── flow-logic.md
│
└── README.md
```

---

## Screenshots

Flow screenshots available under:

```text
screenshots/
```

---

## Setup Instructions

Refer:

```text
docs/setup-guide.md
```

---

## Documentation

- Business Scenario
- Setup Guide
- Architecture
- Flow Logic

Available inside:

```text
docs/
```

---

## Future Enhancements

- Teams notifications
- Multi-level approvals
- SLA-based escalations
- Approval analytics dashboard

---

## Author

Arunkumar R  
Dynamics 365 CRM & Power Platform Developer
