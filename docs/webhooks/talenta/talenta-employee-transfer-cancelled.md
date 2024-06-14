---
layout: page
title: Notify users when cancel transfer employee employee
permalink: /webhooks/talenta/talenta-employee-transfer-cancelled
nav_order: 5
parent: Talenta
grand_parent: Webhooks
---

# Notify users when cancel transfer employee employee

## Prequisite to consume
{: .fw-300 }
1. If there is a employee transfer cancelled

## Event
{: .fw-300 }
```
talenta.employee.transfer.cancelled
```

## Schema
{: .fw-300 }

```javascript
{
    "user_id": Number,
    "employment": {
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
        "join_date": String,
        "length_of_service": String,
        "grade": String,
        "class": String,
        "approval_line": Number,
        "approval_line_employee_id": String,
        "status": String,
        "resign_date": String,
        "working_experiences": Array
    }
}
```

## Example Response
{: .fw-300 }

```json
{
    "user_id": 12321412,
    "employment": {
        "employee_id": "SDET-001",
        "company_id": 3053,
        "organization_id": 20392,
        "organization_name": "IT Division",
        "job_position_id": 20392,
        "job_position": "Staff IT",
        "job_level_id": 20392,
        "job_level": "Manager",
        "employement_status_id": 20392,
        "employment_status": "employment status dont delete",
        "branch_id": 0,
        "branch": "Pusat",
        "join_date": "2018-01-08",
        "length_of_service": "3 Year 10 Month 1 Day",
        "grade": "Grade 1",
        "class": "Class A",
        "approval_line": 935853,
        "approval_line_employee_id": "SDET-002",
        "status": "Active",
        "resign_date": "",
        "working_experiences": []
    },
}
```