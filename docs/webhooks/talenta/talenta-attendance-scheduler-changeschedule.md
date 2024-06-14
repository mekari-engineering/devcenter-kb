---
layout: page
title: Attendance Scheduler Change Schedule
permalink: /webhooks/talenta/talenta-attendance-scheduler-changeschedule
nav_order: 12
parent: Talenta
grand_parent: Webhooks
---

# Attendance Scheduler Change Schedule

## Event
{: .fw-300 }
```
talenta.attendance.scheduler.changeschedule
```

## Schema
{: .fw-300 }

```javascript
{
 "company_id": Number,
 "changes": [
   {
     "schedule_id": Number,
     "schedule_name": String,
     "effective date": String
     "employee_id": String,
     "employee_name":String,
     "user_id": Number,
     "shifts": [
       {
         "pattern_order": Number,
         "shift_name": String,
         "schedule_in": String,
         "schedule_out": String,
         "break_start": String,
         "break_end": String
       },
       {
         "pattern_order": Number,
         "shift_name": String,
         "schedule_in": String,
         "schedule_out": String,
         "break_start": String,
         "break_end": String
       }
     ]
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
     "schedule_id": 123213132,
     "schedule_name": "Jadwal kerja pool",
     "effective date": "23-12-2024",
     "employee_id": "emp001",
     "employee_name": "asep",
     "user_id": 1212,
     "shifts": [
       {
         "pattern_order": 1,
         "shift_name": "shift pagi",
         "schedule_in": "08:00",
         "schedule_out": "17:00",
         "break_start": "12:00",
         "break_end": "13:00"
       },
       {
         "pattern_order": 2,
         "shift_name": "shift siang",
         "schedule_in": "12:00",
         "schedule_out": "20:00",
         "break_start": "16:00",
         "break_end": "17:00"
       }
     ]
   }
   ]
}
```