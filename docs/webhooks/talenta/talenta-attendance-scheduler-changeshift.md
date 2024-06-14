---
layout: page
title: Attendance Scheduler Change Shift
permalink: /webhooks/talenta/talenta-attendance-scheduler-changeshift
nav_order: 12
parent: Talenta
grand_parent: Webhooks
---

# Attendance Scheduler Change Shift

## Event
{: .fw-300 }
```
talenta.attendance.scheduler.changeshift
```

## Schema
{: .fw-300 }

```javascript
{
  "company_id": Number,
  "changes": [
    {
      "date": String,
      "employee_name": String,
      "employee_id":String,
      "user_id": Number,
      "old_shift": {
        "shift id": Number,
        "shift name": String,
        "schedule_in": String,
        "schedule_out": String,
        "break_start": String,
        "break_end": String
      },
      "new_shift": {
        "shift id": Number,
        "shift name": String,
        "schedule_in": String,
        "schedule_out": String,
        "break_start": String,
        "break_end": String
      }
    }
  ]
}
```

## Example Response
{: .fw-300 }

```json
{
  "company_id": 1212,
  "changes": [
    {
      "date": "23-12-2024",
      "employee_name": "emp001",
      "employee_id": "asep",
      "user_id": 1212,
      "old_shift": {
        "shift id": 1231321,
        "shift name": "pagi",
        "schedule_in": "08:00",
        "schedule_out": "17:00",
        "break_start": "12:00",
        "break_end": "13:00"
      },
      "new_shift": {
        "shift id": 3213131,
        "shift name": "malam",
        "schedule_in": "17:00",
        "schedule_out": "23:00",
        "break_start": "20:00",
        "break_end": "21:00"
      }
    }
  ]
}
```