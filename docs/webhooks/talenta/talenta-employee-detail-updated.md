---
layout: page
title: Notify users when updated data employee
permalink: /webhooks/talenta/talenta-employee-detail-updated
nav_order: 2
parent: Talenta
grand_parent: Webhooks
---

# Notify users when updated data employee

## Prequisite to consume
{: .fw-300 }
The event will be triggered when
1. There is a data that edited by client via single edit
1. There is a data that edited by client vi bulk edit
1. Employee transfer is executed or cancelled that impact to the employee detail
1. Resignation created

## Event
{: .fw-300 }
```
talenta.employee.detail.updated
```

## Schema
{: .fw-300 }

```javascript
{
  "user_id": Number,
  "personal": {
    "first_name": String,
    "last_name": String,
    "barcode": String,
    "email": String,
    "identity_type": String
  },
  "family": {
    "members": [
      {
        "id": Number,
        "full_name": String,
        "relationship": String,
        "relationship_id": Number
      }
    ],
    "emergency_contacts": [
      {
        "full_name": String,
        "relationship": String
      }
    ]
  },
  "education": {
      "formal_education_history": [
        {
          "education_degree": String,
          "institution_name": String,
          "majors": String,
          "year_from": String,
          "year_to": String,
          "score": String
        }
      ],
      "informal_education_history": [
        {
          "id": Number,
          "user_id": Number,
          "company_id": Number
        }
      ]
  },
  "employment": {
    "employee_id": String,
    "company_id": Number,
    "organization_id": Number,
    "organization_name": String
    "sign_date": Date,
    "sbu": [
      {
        "field_id": Number,
        "field_name": String,
        "value_id": null,
        "value_name": null,
        "value_code": null
      }
    ]
  },
  "payroll_info": {
    "bpjs_ketenagakerjaan": String,
    "bpjs_kesehatan": String,
    "npwp": String
  },
  "custom_field": [
    {
      "field_name": String,
      "value": String
    }
  ],
  "access_role": {
    "id": Number,
    "name": String
  }
}
```

## Example Response
{: .fw-300 }

```json
{
  "user_id": 12321412,
  "personal": {
    "first_name": "SDET",
    "last_name": "Superadmin",
    "barcode": "MKR861",
    "email": "sdet-automation+test61@mekari.com",
    "identity_type": "KTP"
  },
  "family": {
    "members": [
      {
        "id": 17536,
        "full_name": "ahmad leo",
        "relationship": "Mother",
        "relationship_id": 11
      }
    ],
    "emergency_contacts": [
      {
        "full_name": "eren yeager",
        "relationship": "Father"
      }
    ]
  },
  "education": {
    "formal_education_history": [
      {
        "education_degree": "String",
        "institution_name": "String",
        "majors": "String",
        "year_from": "String",
        "year_to": "String",
        "score": "String"
      }
    ],
    "informal_education_history": [
      {
        "id": 3254,
        "user_id": 935848,
        "company_id": 3053
      }
    ]
  },
  "employment": {
    "employee_id": "SDET-001",
    "company_id": 3053,
    "organization_id": 20392,
    "organization_name": "IT Division",
    "sign_date": "2024-04-16",
    "sbu": [
      {
        "field_id": 4,
        "field_name": "group 1",
        "value_id": null,
        "value_name": null,
        "value_code": null
      }
    ]
  },
  "payroll_info": {
    "bpjs_ketenagakerjaan": "",
    "bpjs_kesehatan": "",
    "npwp": ""
  },
  "custom_field": [
    {
      "field_name": "level",
      "value": ""
    }
  ],
  "access_role": {
    "id": 1,
    "name": "Super Admin"
  }
}
```