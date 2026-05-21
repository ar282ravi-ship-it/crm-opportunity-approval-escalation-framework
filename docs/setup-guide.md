# Setup Guide

## Prerequisites

Before importing the solution ensure:

- Dynamics 365 CRM environment is available
- Power Automate access is enabled
- Outlook connector permissions are available
- Approval connector permissions are enabled

---

## Custom Columns Required

Create the following columns in Opportunity table:

| Column Name | Type | Purpose |
|-------------|------|----------|
| Approval Status | Choice/Text | Stores approval state |
| Discount Percentage | Decimal Number | Stores discount percentage |
| Reminder Count | Whole Number | Tracks reminder attempts |

---

## Trigger Configuration

Table:
`Opportunity`

Trigger:
`When a row is added, modified or deleted`

Settings:

### Change Type
`Added or Modified`

### Scope
`Organization`

### Select Columns
```text
estimatedvalue, discountpercentage, approvalstatus
```

### Filter Rows
```text
estimatedvalue gt 500000 or discountpercentage gt 15
```

---

## Approval Logic

### Step 1
Create manager approval request.

### Step 2
Wait for manager response.

### Step 3
If manager ignores request:

- Send reminder mail every 24 hours
- Increment reminder count

### Step 4
If reminder count >= 2:

Escalate approval to senior manager.

### Step 5
Update opportunity status:

- Approved
- Rejected
- Escalated

---

## Do Until Configuration

### Count
`5`

### Timeout
`P5D`

This prevents infinite looping and limits reminder attempts.

---

## Importing Solution

1. Open Power Apps
2. Navigate to Solutions
3. Click Import Solution
4. Upload ZIP package from:

```text
solution/CRMOpportunityApprovalFramework_1_0_0_1.zip
```

5. Configure connections
6. Turn on the flow
