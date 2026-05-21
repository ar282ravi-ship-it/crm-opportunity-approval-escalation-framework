# Solution Architecture

## Overview

The Opportunity Approval Escalation Framework automates managerial approvals for high-value opportunities in Dynamics 365 CRM using Power Automate.

The framework ensures:

- Automatic approval routing
- Reminder notifications
- Escalation handling
- Status tracking inside CRM

---

## Components Used

### Dynamics 365 CRM
Used to store opportunity data and approval status.

### Power Automate
Used to orchestrate workflow automation.

### Approval Connector
Used to send approval requests.

### Outlook Connector
Used to send reminder and notification emails.

---

## Workflow Architecture

```text
Opportunity Updated
        |
        v
Check Threshold Conditions
(Revenue / Discount)
        |
        v
Manager Approval Request
        |
        +----------------------+
        |                      |
        v                      v
Manager Approves        No Response
        |                      |
        v                      v
Update CRM Status       Reminder Loop
Approved                (Every 24 Hours)
                               |
                               v
                    Reminder Count >= 2
                               |
                               v
                     Escalate to Senior Manager
                               |
                     +---------+---------+
                     |                   |
                     v                   v
                  Approve             Reject
                     |                   |
                     v                   v
              Update CRM Status   Update CRM Status
```

---

## Key Flow Logic

### Trigger Layer

The flow starts when:

- Opportunity record is created
- Opportunity record is modified

The trigger evaluates:

- Estimated Revenue
- Discount Percentage

---

### Approval Layer

The manager receives approval request.

Possible outcomes:

- Approve
- Reject
- Ignore

---

### Reminder Layer

If no response is received:

- Reminder email sent every 24 hours
- Reminder count incremented

---

### Escalation Layer

If reminder threshold reaches 2:

Approval automatically escalates to senior manager.

---

### Status Management

The opportunity record updates dynamically:

| Scenario | Status |
|----------|--------|
| Approved | Approved |
| Rejected | Rejected |
| Escalated | Escalated |

---

## Security Considerations

- Role-based approvals
- Controlled access through CRM security roles
- Approval audit trail maintained
