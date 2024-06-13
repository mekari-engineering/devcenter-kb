---
layout: page
title: Delete Company
permalink: /webhooks/qontak/qontak-crm-company-delete
nav_order: 7
parent: Qontak
grand_parent: Webhooks
---

# 7. Delete Company
Notify user when Company is deleted from Qontak CRM

## Event
{: .fw-300 }
```
qontak.crm.company.delete
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
  "id": 14,
  "name": "PT. CCA engineering",
  "slug": "149c8f2e-a859-4f3d-9a81-5aeeed6bccaf",
}
```