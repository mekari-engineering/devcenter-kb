---
layout: page
title: Notify users when add new employee
permalink: /webhooks/talenta/talenta-employee-detail-created
nav_order: 1
parent: Talenta
grand_parent: Webhooks
---

# Notify users when add new employee

## Prequisite to consume
{: .fw-300 }
The event will be triggered when
1. There is a new employee via bulk update
1. There is a new employee via add new employee
1. There is a new employee added after approval process

## Event
{: .fw-300 }
```
talenta.employee.detail.created
```

## Schema
{: .fw-300 }

```javascript
{
  "personal": {
    "first_name": String,
    "last_name": String,
    "barcode": String,
    "email": String,
    "identity_type": String,
    "identity_number": String,
    "expired_date_identity_id": String,
    "postal_code": String,
    "address": String,
    "current_address": String,
    "birth_place": String,
    "birth_date": Date,
    "phone": String,
    "mobile_phone": String,
    "gender": String,
    "marital_status": String,
    "blood_type": String,
    "religion": String,
    "avatar": String
  },
  "family": {
    "members": [
      {
        "id": Number,
        "full_name": String,
        "relationship": String,
        "relationship_id": Number,
        "birth_date": Date,
        "no_ktp": String,
        "marital_status": String,
        "gender": String,
        "job": String,
        "religion": String,
        "is_deleted": Number,
        "created_at": Date,
        "updated_at": Date
      },
      {
        "id": Number,
        "full_name": String,
        "relationship": String,
        "relationship_id": Number,
        "birth_date": Date,
        "no_ktp": String,
        "marital_status": String,
        "gender": String,
        "job": String,
        "religion": String,
        "is_deleted": Number,
        "created_at": String,
        "updated_at": String
      },
      {
        "id": Number,
        "full_name": String,
        "relationship": String,
        "relationship_id": Number,
        "birth_date": Date,
        "no_ktp": String,
        "marital_status": String,
        "gender": String,
        "job": String,
        "religion": String,
        "is_deleted": Number,
        "created_at": String,
        "updated_at": String
      }
    ],
    "emergency_contacts": [
      {
        "full_name": String,
        "relationship": String,
        "birth_date": String,
        "no_ktp": String,
        "marital_status": String,
        "gender": String,
        "job": String,
        "religion": String
      },
      {
        "full_name": String,
        "relationship": String,
        "birth_date": String,
        "no_ktp": String,
        "marital_status": String,
        "gender": String,
        "job": String,
        "religion": String
      }
    ]
  },
  "education": {
    "formal_education_history": [
    {
      "education_degree": String,
      "institution_name":  String,
      "majors": String,
      "year_from": String,
      "year_to": String,
      "score": String
    }
    ],
    "informal_education_history": [{
      "id": Number,
      "user_id": Number,
      "company_id": Number,
      "held_by_institution_name": String,
      "name": String,
      "duration": Number,
      "duration_type": Number,
      "fee": String,
      "certification": Boolean,
      "start_date": Date,
      "end_date": Date,
      "reference_id": Number,
      "filename": String,
      "description": String,
      "create_date": Date,
      "update_date": Date
      }
    ]
  },
  "employment": {
    "employee_id": String,
    "company_id": Number,
    "organization_id": Number,
    "organization_name": String,
    "job_position_id": Number,
    "job_position": String,
    "job_level_id": Number,
    "job_level": String,
    "employement_status_id": Number,
    "employment_status": String,
    "branch_id": Number,
    "branch": String,
    "join_date": Date,
    "length_of_service": String,
    "grade": String,
    "class":String,
    "approval_line": Number,
    "approval_line_employee_id": String,
    "status": String,
    "resign_date": String,
    "working_experiences": [],
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
    "npwp": String,
    "bank_id": Number,
    "bank_name": String,
    "bank_account": String,
    "bank_account_holder": String,
    "ptkp_status": "TK/0",
    "bank_code": String,
    "cost_center_id": Number,
    "cost_center_name": String,
    "cost_center_category_id": Number,
    "cost_center_category_name": String,
    "employee_tax_status": Number,
    "nationality_code": String,
    "expatriatedn_date": String,
    "created_at": Date,
    "updated_at": Date
  },
  "custom_field": [
    {
      "field_name": Date,
      "value": String
    }
  ],
  "access_role": {
    "id": Number,
    "name": String,
    "role_id": Number,
    "role_name": String,
    "role_type": String
  }
}
```

## Example Response
{: .fw-300 }

```json
{
  "personal": {
    "first_name": "SDET",
    "last_name": "Superadmin",
    "barcode": "MKR861",
    "email": "sdet-automation+test61@mekari.com",
    "identity_type": "KTP",
    "identity_number": "",
    "expired_date_identity_id": "",
    "postal_code": "",
    "address": "",
    "current_address": "",
    "birth_place": "Johor Baru",
    "birth_date": "1992-07-08",
    "phone": "",
    "mobile_phone": "",
    "gender": "Male",
    "marital_status": "Married",
    "blood_type": "AB",
    "religion": "Islam",
    "avatar": "https://development-test2.s3.ap-southeast-1.amazonaws.com/avatar/24INn05dp_aR9P2_LdZrPmLWKLPUDYbL.png?X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Security-Token=FwoGZXIvYXdzECIaDCN2L8MBwg%2B0LRKuIiLDAXiMYm5A4AEHNaunWBbuIn6ZUBzmOVQvvj1VBlYNYxQHAGQEL%2F4RNQcTyzQCs8%2B%2BCXzRwpdBPGOtX%2BXRQ05cFxJkdeW3VXEBhTzb3tAN3Zl1qwLySB9rxFO8JbU9GvcSSezSGuf1ieqQlzfexueuH%2Fss02Juxj2ZoX4YOTYmrZty3XEBIDtLALvWmzTD6%2BAjfKWRziOWYfG9PQ2BMvgO4qXPkw2wTXqCdaVdR5m4nErSzT%2BnVegxXnbyH53xuf2xays%2BTCi3z6OMBjIt0wIwyHTK7NNFbTg5iAKLx9IQNjaqu0KRqdIE7UVLFKjQLYe%2Bv4uBOVW3cP7f&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIA3A7QLOC3I44ZUHDE%2F20211108%2Fap-southeast-1%2Fs3%2Faws4_request&X-Amz-Date=20211108T090648Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1800&X-Amz-Signature=4327cc2f9e851f12724ed4076fdd05d3950ab4b730e9bfd671a714ceff21ec7c"
  },
  "family": {
    "members": [
      {
        "id": 17536,
        "full_name": "ahmad leo",
        "relationship": "Mother",
        "relationship_id": 11,
        "birth_date": "2021-09-06",
        "no_ktp": "",
        "marital_status": "",
        "gender": "Male",
        "job": "",
        "religion": "",
        "is_deleted": 0,
        "created_at": "2021-09-06 15:11:14",
        "updated_at": "2021-09-06 15:11:14"
      },
      {
        "id": 17545,
        "full_name": "Sekala Niskala",
        "relationship": "Sibling",
        "relationship_id": 2,
        "birth_date": "1990-12-05",
        "no_ktp": "310202010101010",
        "marital_status": "Married",
        "gender": "Male",
        "job": "Detektif Swasta",
        "religion": "Catholic",
        "is_deleted": 0,
        "created_at": "2021-09-22 12:34:35",
        "updated_at": "2021-09-22 12:34:35"
      },
      {
        "id": 17546,
        "full_name": "Akan didelete",
        "relationship": "Cousin",
        "relationship_id": 20,
        "birth_date": "1944-02-16",
        "no_ktp": "",
        "marital_status": "",
        "gender": "Female",
        "job": "",
        "religion": "",
        "is_deleted": 1,
        "created_at": "2021-09-22 12:37:29",
        "updated_at": "2021-09-22 12:43:38"
      }
    ],
    "emergency_contacts": [
      {
        "full_name": "eren yeager",
        "relationship": "Father",
        "birth_date": "",
        "no_ktp": "",
        "marital_status": "",
        "gender": "",
        "job": "",
        "religion": ""
      },
      {
        "full_name": "Sekala Niskala",
        "relationship": "Sibling",
        "birth_date": "",
        "no_ktp": "",
        "marital_status": "",
        "gender": "",
        "job": "",
        "religion": ""
      }
    ]
  },
  "education": {
    "formal_education_history": [
    {
      "education_degree": "String",
      "institution_name": "String",
      "majors":"String",
      "year_from":"String",
      "year_to":"String",
      "score":"String"
    }
    ],
    "informal_education_history": [{
      "id": 3254,
      "user_id": 935848,
      "company_id": 3053,
      "held_by_institution_name": "Lembaga Iusto.",
      "name": "Course Et.",
      "duration": 31,
      "duration_type": 1,
      "fee": "118329",
      "certification": true,
      "start_date": "2021-12-27",
      "end_date": "2022-01-26",
      "reference_id": 28,
      "filename": "https://development-test2.s3.ap-southeast-1.amazonaws.com/myinfo/training/wLQJlpLmUnsNs_eBKI8nsxdZYOAC2zyx.png?X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Security-Token=FwoGZXIvYXdzEGIaDEHJfsTsVA9hzVtPoiLDATIPTwZqJeLdMPBLd62hpNghK7HvUCETforSrmSQrYeGlj6mPcFVIhj2Rb7lS0D79BMdFjcSghrrR%2BKRlrVV1knhlcXtaRlF5gLulIfX7Qk00f5mjrWeIxJ1HEIcSA2AkXgzDE57yr50nwtDSyfUIQYgBcD%2FZ%2B%2BIPxq03ig6jRa29Z6rM23bVxLliH%2BZ3U6GOEUsPTQ7Rhnr1QhPJ3YvUm7pizf9nSI0uvCbe0dbwvZAA7Rw9bmHTBxPceWVJ6v%2BonQjwyi3yvOPBjItznPnejlaj2WDqSop0O5HpBVdp2V5Tc5QTlxPz4daK9NZGkMaid2uXiINv5AW&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIA3A7QLOC3AF6TD7NE%2F20220204%2Fap-southeast-1%2Fs3%2Faws4_request&X-Amz-Date=20220204T083720Z&X-Amz-SignedHeaders=host&X-Amz-Expires=1800&X-Amz-Signature=7f422cd28f47ac5ccdec439f74bb1b91f07945eaa43da46a75be18c5909e6dfb",
      "description": "",
      "create_date": "2022-01-27 10:40:09",
      "update_date": "2022-01-27 10:40:09"
      }
    ]
  },
  "employment": {
    "employee_id": "SDET-001",
    "company_id": 3053,
    "organization_id": 20392,
    "organization_name": "IT Division",
    "job_position_id": 20392,
    "job_position": "Staff IT",
    "job_level_id": 20392,
    "job_level": "Manager",
    "employement_status_id": 20392,
    "employment_status": "employment status dont delete",
    "branch_id": 0,
    "branch": "Pusat",
    "join_date": "2018-01-08",
    "length_of_service": "3 Year 10 Month 1 Day",
    "grade": "Grade 1",
    "class": "Class A",
    "approval_line": 935853,
    "approval_line_employee_id": "SDET-002",
    "status": "Active",
    "resign_date": "",
    "working_experiences": [],
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
    "npwp": "",
    "bank_id": 0,
    "bank_name": "-",
    "bank_account": "",
    "bank_account_holder": "",
    "ptkp_status": "TK/0",
    "bank_code": "",
    "cost_center_id": 71,
    "cost_center_name": "COST CENTER DONT DELETE",
    "cost_center_category_id": 1,
    "cost_center_category_name": "Direct",
    "employee_tax_status": 0,
    "nationality_code": "",
    "expatriatedn_date": "",
    "created_at": "2020-11-13 14:11:56",
    "updated_at": "2021-10-19 17:30:22"
  },
  "custom_field": [
    {
      "field_name": "level",
      "value": ""
    }
  ],
  "access_role": {
    "id": 1,
    "name": "Super Admin",
    "role_id": 1,
    "role_name": "Super Admin",
    "role_type": "default"
  }
}
```