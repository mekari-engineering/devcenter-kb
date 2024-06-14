---
layout: page
title: Add Company
permalink: /webhooks/qontak/qontak-crm-company-create
nav_order: 5
parent: Qontak
grand_parent: Webhooks
---

# Add Company
Notify user when new Company is created/added in Qontak CRM

## Event
{: .fw-300 }
```
qontak.crm.company.create
```

## Schema
{: .fw-300 }

```javascript
 {
  "id": Number,
  "slug": String,
  "name": String,
  "website": String,
  "created_at": {"type": String,"format": Date},
  "updated_at": {"type": String,"format": Date},
  "creator_id": Number,
  "creator_name": String,
  "telephone": String,
  "address": String,
  "country": String,
  "province": String,
  "city": String,
  "zipcode": String,
  "industry_id": Number,
  "industry_name": String,
  "crm_type_id": Number,
  "crm_type_name": String,
  "number_of_employees": Number,
  "crm_source_id": Number,
  "crm_source_name": String,
  "annual_revenue": String,
  "business_reg_number": String,
  "crm_deal_ids": [
    Number  
  ],
  "crm_deal_name": [
    String  
  ],
  "crm_person_ids": [
    Number
  ],
  "crm_person_name": [
    String
  ],
  "ancestry": String,
  "unique_company_id": String,
  "additional_fields": [
    {
      "id": Number,
      "name": String,
      "value": String,
      "value_name": String
    }
  ]
}
```

## Example Response
{: .fw-300 }

```json
{
  "id": "integer",
  "slug": "string",
  "name": "string",
  "website": "string",
  "created_at": {"type": "string","format": "date-time"},
  "updated_at": {"type": "string","format": "date-time"},
  "creator_id": "integer",
  "creator_name": "string",
  "telephone": "string",
  "address": "string",
  "country": "string",
  "province": "string",
  "city": "string",
  "zipcode": "string",
  "industry_id": "integer",
  "industry_name": "string",
  "crm_type_id": "integer",
  "crm_type_name": "string",
  "number_of_employees": "integer",
  "crm_source_id": "integer",
  "crm_source_name": "string",
  "annual_revenue": "string",
  "business_reg_number": "string",
  "crm_deal_ids": [
    "integer"  
  ],
  "crm_deal_name": [
    "string"  
  ],
  "crm_person_ids": [
    "integer"
  ],
  "crm_person_name": [
    "string"
  ],
  "ancestry": "string",
  "unique_company_id": "string",
  "additional_fields": [
    {
      "id": "integer",
      "name": "string",
      "value": "string",
      "value_name": "string"
    }
  ]
}
```