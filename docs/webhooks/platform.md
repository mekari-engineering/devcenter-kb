---
layout: page
title: Platform
permalink: /webhooks/platform
nav_order: 1
parent: Webhooks
---

# 1. Send user logout activity log

## Prequisite to consume
{: .fw-300 }
1. Company request to get their employee activity log through AD-Hoc
1. SSO will add a flag of `send_webhook_activity_log=true` on the company metadata
1. Company employee successfully logout on SSO (this will trigger to send to Webhook Service)

## Event
{: .fw-300 }
```
platform.authentication.logoff
```

## Schema
{: .fw-300 }

```javascript
{
  activity_name: String,
  activity_id: Number,
  auth_protocol: String,
  auth_protocol_id: Number,
  category_name: String,
  category_uid: Number,
  class_name: String,
  class_uid: Number,
  time: String,
  metadata: {
    uid: String,
    product: {
      name: String,
      vendor_name: String,
    },
    version: String,
  },
  severity: String,
  severity_id: Number,
  type_uid: Number,
  type_name: String,
  user: {
    uid: String,
    email_addr: String,
    full_name: String,
    type: String,
    type_id: Number
  },
  timezone_offset: Number,
  status: String,
  status_id: Number,
  status_detail: String,
  is_remote: Boolean,
  is_cleartext: Boolean
}
```

## Example Response
{: .fw-300 }

```json
{
  "id": 1,
  "user_id": 9611,
  "template_id": 1,
  "created_date": "2023-01-01 00:00:00",
  "updated_date": "2023-01-01 00:00:00",
  "status": 1,
  "last_approval_id": 8002,
  "request_detail": [
    {
      "id": 1,
      "question_id": 1,
      "type": 10,
      "value": "2023-01-01"
    },
    {
      "id": 2,
      "question_id": 2,
      "type": 4,
      "value": "XL"
    },
    {
      "id": 3,
      "question_id": 3,
      "type": 4,
      "value": "Yes"
    },
    {
      "id": 4,
      "question_id": 4,
      "type": 4,
      "value": "Yes"
    },
    {
      "id": 5,
      "question_id": 5,
      "type": 11,
      "value": "Lorem Ipsum"
    }
  ],
  "template": {
    "id": 1,
    "name": "Form Pengajuan Loan",
    "creator": 8002,
    "company_id": 679,
    "category": 3
  },
  "loan": {
    "loan_name_id": 123
  }
}
```

# 2. Send user login activity log

## Prequisite to consume
{: .fw-300 }
1. Company request to get their employee activity log through AD-Hoc
1. SSO will add a flag of `send_webhook_activity_log=true` on the company metadata
1. Company employee successfully login to SSO (this will trigger to send to Webhook Service)

## Event
{: .fw-300 }
```
platform.authentication.logon
```

## Schema
{: .fw-300 }

```javascript
{
  activity_name: String,
  activity_id: Number,
  auth_protocol: String,
  auth_protocol_id: Number,
  category_name: String,
  category_uid: Number,
  class_name: String,
  class_uid: Number,
  time: String,
  metadata: {
    uid: String,
    product: {
      name: String,
      vendor_name: String,
    },
    version: String,
  },
  severity: String,
  severity_id: Number,
  type_uid: Number,
  type_name: String,
  user: {
    uid: String,
    email_addr: String,
    full_name: String,
    type: String,
    type_id: Number
  },
  timezone_offset: Number,
  status: String,
  status_id: Number,
  status_detail: String,
  is_remote: Boolean,
  is_cleartext: Boolean
}
```

## Example Response
{: .fw-300 }

```json
{
  "id": 1,
  "user_id": 9611,
  "template_id": 1,
  "created_date": "2023-01-01 00:00:00",
  "updated_date": "2023-01-01 00:00:00",
  "status": 1,
  "last_approval_id": 8002,
  "request_detail": [
    {
      "id": 1,
      "question_id": 1,
      "type": 10,
      "value": "2023-01-01"
    },
    {
      "id": 2,
      "question_id": 2,
      "type": 4,
      "value": "XL"
    },
    {
      "id": 3,
      "question_id": 3,
      "type": 4,
      "value": "Yes"
    },
    {
      "id": 4,
      "question_id": 4,
      "type": 4,
      "value": "Yes"
    },
    {
      "id": 5,
      "question_id": 5,
      "type": 11,
      "value": "Lorem Ipsum"
    }
  ],
  "template": {
    "id": 1,
    "name": "Form Pengajuan Loan",
    "creator": 8002,
    "company_id": 679,
    "category": 3
  },
  "loan": {
    "loan_name_id": 123
  }
}
```