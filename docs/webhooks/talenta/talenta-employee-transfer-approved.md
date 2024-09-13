---
layout: page
title: Notify users when approved transfer employee
permalink: /webhooks/talenta/talenta-employee-transfer-approved
nav_order: 4
parent: Talenta
grand_parent: Webhooks
---

# Notify users when approved transfer employee

## Prequisite to consume
{: .fw-300 }
1. If there is a employee transfer approved

## Event
{: .fw-300 }
```
talenta.employee.transfer.approved
```

## Schema
{: .fw-300 }

```javascript
{
    "user_id": Number,
    "old_employment": {
        "effective date": String,
        "employee_id": String,
        "company_id": Number,
        "organization_id": Number,
        "organization_name": String,
        "job_position_id": Number,
        "job_position": String,
        "job_level_id": Number,
        "job_level": String,
        "employement_status_id": Number,
        "employment_status": String,
        "branch_id": Number,
        "branch": String,
        "grade": String,
        "class": String,
        "approval_line": Number,
        "approval_line_employee_id": String,
        "status": String,
        "effective_date": String,
    },
    "new_employment": {
        "effective date": String,
        "employee_id": String,
        "company_id": Number,
        "organization_id": Number,
        "organization_name": String,
        "job_position_id": Number,
        "job_position": String,
        "job_level_id": Number,
        "job_level": String,
        "employement_status_id": Number,
        "employment_status": String,
        "branch_id": Number,
        "branch": String,
        "grade": String,
        "class": String,
        "approval_line": Number,
        "approval_line_employee_id": String,
        "status": String,
        "effective_date": String,
    }
}
```

## Example Response
{: .fw-300 }

```json
{
    "user_id": "integer",
    "old_employment": {
        "effective date": "string",
        "employee_id": "string",
        "company_id": "integer",
        "organization_id": "integer",
        "organization_name": "string",
        "job_position_id": "integer",
        "job_position": "string",
        "job_level_id": "integer",
        "job_level": "string",
        "employement_status_id": "integer",
        "employment_status": "string",
        "branch_id": "integer",
        "branch": "string",
        "grade": "string",
        "class": "string",
        "approval_line": "integer",
        "approval_line_employee_id": "string",
        "status": "string",
        "effective_date": "string",
    },
    "new_employment": {
        "effective date": "string",
        "employee_id": "string",
        "company_id": "integer",
        "organization_id": "integer",
        "organization_name": "string",
        "job_position_id": "integer",
        "job_position": "string",
        "job_level_id": "integer",
        "job_level": "string",
        "employement_status_id": "integer",
        "employment_status": "string",
        "branch_id": "integer",
        "branch": "string",
        "grade": "string",
        "class": "string",
        "approval_line": "integer",
        "approval_line_employee_id": "string",
        "status": "string",
        "effective_date": "string",
    }
}
```