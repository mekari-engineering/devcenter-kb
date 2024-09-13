---
layout: page
title: Create Loan based on form submission
permalink: /webhooks/talenta/talenta-forms-entry-approved
nav_order: 8
parent: Talenta
grand_parent: Webhooks
---

# Create Loan based on form submission

## Prequisite to consume
{: .fw-300 }
The event will be triggered when
- certain form submission is approved by the approval

## Event
{: .fw-300 }
```
talenta.forms.entry.approved
```

## Schema
{: .fw-300 }

```javascript
{
  "request": {
    "id": Number,
    "user_id": Number,
    "template_id": Number,
    "created_date": Timestamp,
    "updated_date": Timestamp,
    "status": Number,
    "last_approval_id": Number,
    "superadmin_sso_id": String,
    "request_detail": [
        {
          "id": Number,
          "question_id": Number,
          "type": Number,
          "value": String
        },
        {
          "id": Number,
          "question_id": Number,
          "type": Number,
          "value": String
        },
        {
          "id": Number,
          "question_id": Number,
          "type": Number,
          "value": String
        },
        {
          "id": Number,
          "question_id": Number,
          "type": Number,
          "value": String
        },
        ...
      ],
    "template": {
      "id": Number,
      "name": String,
      "creator": Number,
      "company_id": Number,
      "category": Number
    },
    "loan": {
      "loan_name_id": Number,
    }
  }
}
```

## Example Response
{: .fw-300 }

```json
{
  "request": {
    "id":1,
    "user_id":9611,
    "template_id":1,
    "created_date":"2023-01-01 00:00:00",
    "updated_date":"2023-01-01 00:00:00",
    "status":1,
    "last_approval_id":8002,
    "superadmin_sso_id": String,
    "request_detail": [
        {
          "id":1,
          "question_id":1,
          "type":10,
          "value":"2023-01-01" // tanggal masuk
        },
        {
          "id":2,
          "question_id":2,
          "type":4,
          "value":"XL" // ukuran baju
        },
        {
          "id":3,
          "question_id":3,
          "type":4,
          "value":"Yes" // butuh topi
        },
        {
          "id":4,
          "question_id":4,
          "type":4,
          "value":"Yes" // butuh apron
        },
        {
          "id":5,
          "question_id":5,
          "type":11,
          "value":"Lorem Ipsum" // Keterangan
        },
      ],
    "template": {
      "id":1,
      "name":"Form Pengajuan Loan",
      "creator":8002,
      "company_id":679,
      "category":3
    },
    "loan": {
      "loan_name_id":123,
    }
  }
}
```