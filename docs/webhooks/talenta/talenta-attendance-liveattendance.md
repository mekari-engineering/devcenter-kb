---
layout: page
title: Live Attendance
permalink: /webhooks/talenta/talenta-attendance-liveattendance
nav_order: 9
parent: Talenta
grand_parent: Webhooks
---

# Live Attendance

## Event
{: .fw-300 }
```
talenta.attendance.liveattendance
```

## Schema
{: .fw-300 }

```javascript
{
   "user_id": Number,
    "employee_id": String,
    "email": String,
    "company_id": Number,
    "date": String,
    "shift": String,
    "schedule_in": ,
    "schedule_out": time,
    "final_check_in": time,
    "final_check_out": time,
    "schedule_break_in": time,
    "schedule_break_out": time,
    "time": timestamp
    "location": String,
    "coordinate": String,
    "description": String,
    "source": String,
    "type": String,
    "locations": [
      {
        "id": Number,
        "setting_id": Number,
        "name": String,
        "radius": Number,
        "latitude": String,
        "longitude": String,
        "address": String,
      }
    ]
}
```

## Example Response
{: .fw-300 }

```json
{
   "user_id": 333312,
    "employee_id": "MKR-1045",
    "email": "teo.wijayarto@mekari.com",
    "company_id": 3620,
    "date": "2021-03-02",
    "shift": "office",
    "schedule_in": "09:00:00",
    "schedule_out": "18:00:00",
    "final_check_in": "18:45:40",
    "final_check_out": "07:00:00",
    "schedule_break_in": "07:00:00",
    "schedule_break_out": "07:00:00",
    "time": "2021-03-02 18:50:01",
    "location": "-",
    "coordinate": "-6.1429812,106.7813307",
    "description": "test production API",
    "source": "Mobile Apps",
    "type": "CI",
    "locations": [
      {
        "id": 1291892,
        "setting_id": 8724,
        "name": "Home",
        "radius": 200,
        "latitude": "-6.209403",
        "longitude": "106.8208889",
        "address": "Chugoku Paints Indonesia PT, Jakarta Pusat 10220, Indonesia",
      }
    ]
}
```