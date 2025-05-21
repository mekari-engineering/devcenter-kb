---
layout: page
title: Send Person or Contact
permalink: /webhooks/jurnal/send-contact
parent: Jurnal
grand_parent: Webhooks
---

# Send Person or Contact to Webhook Consumer Every New Contact Created

## Prequisite to Consume
{: .fw-300 }
1. Feature contact webhook for that company is active in [Jurnal](https://jurnal.id)
2. User need to create new contact

## Event
{: .fw-300 }
```
jurnal.person.created
```

## Schema
{: .fw-300 }

```json
{
  "id": "integer",
  "display_name": "string",
  "title": "string",
  "first_name": "string",
  "middle_name": "string",
  "last_name": "string",
  "fullname_with_title": "string",
  "mobile": "string",
  "identity_type": "string",
  "identity_number": "string",
  "email": "string",
  "other_detail": "string",
  "associate_company": "string",
  "phone": "string",
  "fax": "string",
  "tax_no": "string",
  "archive": "string",
  "billing_address": "string",
  "billing_address_no": "string",
  "billing_address_rt": "string",
  "billing_address_rw": "string",
  "billing_address_post_code": "string",
  "billing_address_kelurahan": "string",
  "billing_address_kecamatan": "string",
  "billing_address_kabupaten": "string",
  "billing_address_provinsi": "string",
  "address": "string",
  "bank_account_details": [
    {
      "bank_name": "string",
      "bank_partner_id": "integer",
      "bank_branch": "string",
      "bank_account_holder_name": "string",
      "bank_account_number": "string",
      "is_valid": "boolean"
    }
  ],
  "default_ar_account_id": "integer",
  "default_ap_account_id": "integer",
  "disable_max_credit_limit": "boolean",
  "disable_max_debit_limit": "boolean",
  "max_credit_limit": "integer",
  "max_debit_limit": "integer",
  "term_id": "integer",
  "is_customer": "boolean",
  "is_vendor": "boolean",
  "is_employee": "boolean",
  "custom_id": "integer",
  "source": "apikey",
  "is_others": "boolean"
}
```

## Example Response
{: .fw-300 }

```json
{
    "id": 834496,
    "display_name": "Bambang",
    "title": null,
    "first_name": null,
    "middle_name": null,
    "last_name": null,
    "fullname_with_title": "",
    "mobile": null,
    "identity_type": "",
    "identity_number": null,
    "email": "",
    "other_detail": null,
    "associate_company": null,
    "phone": null,
    "fax": null,
    "tax_no": null,
    "archive": false,
    "billing_address": null,
    "billing_address_no": "",
    "billing_address_rt": "",
    "billing_address_rw": "",
    "billing_address_post_code": "",
    "billing_address_kelurahan": "",
    "billing_address_kecamatan": "",
    "billing_address_kabupaten": "",
    "billing_address_provinsi": "",
    "address": null,
    "bank_account_details": [
      {
        "bank_name": null,
        "bank_partner_id": 0,
        "bank_branch": "",
        "bank_account_holder_name": "",
        "bank_account_number": "",
        "is_valid": null
      }
    ],
    "default_ar_account_id": 30918189,
    "default_ap_account_id": 30918196,
    "disable_max_credit_limit": true,
    "disable_max_debit_limit": true,
    "max_credit_limit": null,
    "max_debit_limit": null,
    "term_id": null,
    "is_customer": true,
    "is_vendor": false,
    "is_employee": false,
    "custom_id": null,
    "source": "apikey",
    "is_others": false
}
```