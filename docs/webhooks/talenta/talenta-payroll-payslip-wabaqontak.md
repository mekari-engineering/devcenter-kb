---
layout: page
title: Payroll Payslip Wabaqontak
permalink: /webhooks/talenta/talenta-payroll-payslip-wabaqontak
nav_order: 11
parent: Talenta
grand_parent: Webhooks
---

# Payroll Payslip Wabaqontak

## Event
{: .fw-300 }
```
talenta.payroll.payslip.wabaqontak
```

## Schema
{: .fw-300 }

```javascript
{
   "user_id": int,
   "employee_id": string,
   "fullname": string,
   "phone_number": string,
   "month":string,
   "year": string,
   "message": string,
   "payslip_link":string,
   "publish_time":timestamp
}
```

## Example Response
{: .fw-300 }

```json
{
   "user_id": 333312,
   "employee_id": "MKR-1045",
   "fullname": "Teo Wijayarto",
   "phone_number": "+628111223344",
   "month": "December",
   "year": "2023",
   "message": "Klik link dibawah untuk mengakses payslip anda.",
   "payslip_link": "https://hr.talenta.co/report/payslip?id=109140993&month=12&year=2023",
   "publish_time":"2023-03-22 12:00:11"
}
```