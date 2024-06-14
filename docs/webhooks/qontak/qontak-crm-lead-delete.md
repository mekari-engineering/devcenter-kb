---
layout: page
title: Delete Contact
permalink: /webhooks/qontak/qontak-crm-lead-delete
nav_order: 10
parent: Qontak
grand_parent: Webhooks
---

# Delete Contact
Notify user when Contact is deleted from Qontak CRM

## Event
{: .fw-300 }
```
qontak.crm.lead.delete
```

## Schema
{: .fw-300 }

```javascript
{
  "id": Number,
  "name": String,
  "slug": String
}
```

## Example Response
{: .fw-300 }

```json
{
  "id": 30,
  "name": "Budi Sudarsono",
  "slug": "149c8f2e-a859-4f3d-9a81-5aasdd6bcca8",
}
```