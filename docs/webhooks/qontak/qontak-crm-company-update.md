---
layout: page
title: Edit Company
permalink: /webhooks/qontak/qontak-crm-company-update
nav_order: 6
parent: Qontak
grand_parent: Webhooks
---

# Edit Company
Notify user when Company is updated in Qontak CRM

## Event
{: .fw-300 }
```
qontak.crm.company.update
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
  "id": 38,
  "slug": "78e434ef-61ce-4667-aa4b-ad9f83e6caa3",
  "name": "Company ZianTech",
  "website": "www.ziantech.com",
  "created_at": "2024-01-12T15:56:35.509+07:00",
  "updated_at": "2024-01-12T17:52:25.911+07:00",
  "creator_id": 2,
  "creator_name": "Ade Saputra",
  "telephone": "6221 23323",
  "address": "Jl. Sesama 10",
  "country": "Indonesia",
  "province": "Jawa Tengah",
  "city": "Tegal",
  "zipcode": "",
  "industry_id": 212,
  "industry_name": "Information Technology and Services",
  "crm_type_id": 3,
  "crm_type_name": "Opportunity",
  "number_of_employees": 300,
  "crm_source_id": null,
  "crm_source_name": null,
  "annual_revenue": null,
  "business_reg_number": "",
  "crm_deal_ids": [
    44
  ],
  "crm_deal_name": [
    "Just Deal"
  ],
  "crm_person_ids": [
    8
  ],
  "crm_person_name": [
    "Hendra Karta"
  ],
  "ancestry": "19",
  "unique_company_id": null,
  "additional_fields": [
    {
      "id": 90,
      "name": "daerah",
      "value": "Margasari",
      "value_name": "Margasari"
    }
  ]
}
```