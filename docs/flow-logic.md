# Flow Logic

## Objective

The flow automates approval management for high-value opportunities in Dynamics 365 CRM.

It ensures:

- Timely approvals
- Reminder notifications
- Escalation management
- Approval tracking

---

## Flow Execution Logic

### Step 1 — Trigger Execution

The flow starts when:

An Opportunity record is:

- Added
- Modified

Trigger checks:

```text
estimatedvalue gt 500000
OR
discountpercentage gt 15
```

If condition is not met:

Flow stops.

---

### Step 2 — Approval Validation

Before creating approval:

System validates:

```text
Approval Status != Approved
AND
Approval Status != Rejected
```

This prevents duplicate approval requests.

---

### Step 3 — Manager Approval Creation

Power Automate creates an approval request for:

```text
Manager
```

Approval type:

```text
Approve/Reject – First to respond
```

Manager actions:

- Approve
- Reject
- Ignore

---

### Step 4 — Reminder Loop

If manager ignores approval:

A `Do Until` loop starts.

Condition:

```text
approvalCompleted = true
```

Inside loop:

1. Wait 24 hours
2. Send reminder email
3. Increment reminder count

---

### Step 5 — Escalation Logic

Condition:

```text
reminderCount >= 2
```

If true:

Approval request escalates to:

```text
Senior Manager
```

CRM status updates to:

```text
Escalated
```

---

### Step 6 — Senior Manager Decision

Possible outcomes:

### Approved

System:

- Updates Opportunity Status → Approved
- Sends approval notification email

### Rejected

System:

- Updates Opportunity Status → Rejected
- Sends rejection notification email

---

### Step 7 — Loop Termination

Do Until exits when:

```text
approvalCompleted = true
```

OR

Maximum limit reached:

Count:
```text
5
```

Timeout:
```text
P5D
```

This prevents infinite execution.

---

## Example Scenarios

### Scenario 1 — Manager Approves Immediately

1. Opportunity exceeds threshold
2. Approval sent to manager
3. Manager approves
4. Status updated → Approved
5. Flow ends

---

### Scenario 2 — Manager Ignores

1. Approval sent
2. Reminder after 24 hours
3. Reminder count increases
4. After 2 reminders:
5. Escalation to senior manager

---

### Scenario 3 — Senior Manager Approves

1. Escalated approval sent
2. Senior manager approves
3. CRM updated → Approved
4. Notification sent
