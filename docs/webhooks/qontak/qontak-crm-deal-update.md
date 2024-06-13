---
layout: page
title: Edit Deals
permalink: /webhooks/qontak/qontak-crm-deal-update
nav_order: 3
parent: Qontak
grand_parent: Webhooks
---

# Edit Deals

## Prequisite to consume
{: .fw-300 }
1. Client also can edit their deal
1. When update the data of deal, we will return all of object deal
1. Which client can edit deals? All client with permission edit deal are Everything

## Event
{: .fw-300 }
```
qontak.crm.deal.update
```

## Schema
{: .fw-300 }

```javascript
{
  "id": Number,
  "name": String,
  "slug": String,
  "created_at": {"type": String,"format": Date},
  "updated_at": {"type": String,"format": Date},
  "currency": String,
  "size": Number, // or null
  "closed_date": {"type": String,"format": Date},
  "creator_id": Number,
  "creator_name": String,
  "crm_source_id": Number, // or null
  "crm_source_name": null,
  "crm_lost_reason_id": Number, // or null
  "crm_lost_reason_name": null,
  "crm_pipeline_id": Number,
  "crm_pipeline_name": String,
  "crm_stage_id": Number,
  "crm_stage_name": String,
  "start_date": {"type": String,"format": Date},
  "expired_date": {"type": String,"format": Date},
  "crm_priority_id": Number,
  "crm_priority_name": String,
  "crm_company_id": [
    Number, // or null
  ],
  "crm_company_name": [
    String,
  ],
  "crm_lead_ids": [
    Number, // or null
  ],
  "crm_lead_name": [
    String,
  ],
  "product_association_ids": [
    Number, // or null
  ],
  "product_association_name": [
    String,
  ],
  "product_association_quantity": "array",
  "product_association_price": "array",
  "product_association_total_price":"array",
  "additional_fields": [
    {
      "id": Number,
      "name": String,
      "value": String,
      "value_name": String,
    },
    {
      "id": Number,
      "name": String,
      "value": String,
      "value_name": String,
    },
  ]
}
```

## Example Response
{: .fw-300 }

```json
{
  "id": 1,
  "name": "Deal A",
  "slug": "deal-A-2934",
  "created_at": "2021-07-13T00:00:00.000+07:00",
  "updated_at": "2021-07-13T00:00:00.000+07:00",
  "currency": "IDR",
  "size": "10000000.0",
  "closed_date": "2021-08-15T00:00:00.000+07:00",
  "creator_id": 1,
  "creator_name": "User 1",
  "crm_source_id": null,
  "crm_source_name": null,
  "crm_lost_reason_id": null,
  "crm_lost_reason_name": null,
  "crm_pipeline_id": 1,
  "crm_pipeline_name": "Sales Pipeline",
  "crm_stage_id": 1,
  "crm_stage_name": "Qualified",
  "start_date": "2021-07-13T00:00:00.000+07:00",
  "expired_date": "2022-03-15T00:00:00.000+07:00",
  "crm_priority_id": 1,
  "crm_priority_name": "Priority 1",
  "crm_company_id": [
    1
  ],
  "crm_company_name": [
    "Zoo"
  ],
  "crm_lead_ids": [
    1
  ],
  "crm_lead_name": [
    "Customer Support"
  ],
  "product_association_ids": [
    1
  ],
  "product_association_name": [
    "Special Package"
  ],
  "product_association_quantity": [],
  "product_association_price": [],
  "product_association_total_price": [],
  "additional_fields": [
    {
      "id": 1,
      "name": "additional_field_1",
      "value": null,
      "value_name": "Value Here"
    },
    {
      "id": 2,
      "name": "additional_field_2",
      "value": null,
      "value_name": "Some Value"
    }
  ]
}
```