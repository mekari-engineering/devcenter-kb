---
layout: page
title: Send Receive Payment
permalink: /webhooks/jurnal/send-receive-payment
parent: Jurnal
grand_parent: Webhooks
---

# Send Receive Payment to Webhook Consumer Every New Receive Payment Created

## Prequisite to Consume
{: .fw-300 }
1. Feature receive payment webhook for that company is active in [Jurnal](https://jurnal.id)
2. User need to create new receive payment

## Event
{: .fw-300 }
```
jurnal.receivepayment.created
```

## Schema
{: .fw-300 }

```json
{
  "id": "integer",
  "transaction_no": "string",
  "token": "string",
  "memo": "string",
  "source": "string",
  "custom_id": "integer",
  "status": "string",
  "transaction_status": {
    "id": "integer",
    "name": "Paid",
    "created_at": {"type": "string","format": "date-time"},,
    "updated_at": {"type": "string","format": "date-time"},,
    "name_bahasa": "string"
  },
  "deleted_at": {"type": "string","format": "date-time"},,
  "audited_by": "string",
  "transaction_date": {"type": "string","format": "date-time"},,
  "due_date": {"type": "string","format": "date-time"},,
  "person": {
    "id": "integer",
    "name": "string",
    "email": "string",
    "address": "string",
    "phone": "string",
    "fax": "string"
  },
  "transaction_type": {
    "id": "integer",
    "name": "string"
  },
  "payment_method": {
    "id": "integer",
    "name": "string"
  },
  "deposit_to": {
    "id": "integer",
    "name": "string",
    "number": "string",
    "category": {
      "id": "integer",
      "name": "string"
    }
  },
  "is_draft": "boolean",
  "proforma_id": "integer",
  "witholding": {
    "witholding_account_name": "string",
    "witholding_account_number": "integer",
    "account_id": "integer",
    "value": "string",
    "type": "string",
    "amount": "integer",
    "amount_currency_format": "string",
    "category": {
      "id": "integer",
      "name": "string"
    }
  },
  "original_amount": "integer",
  "original_amount_currency_format": "string",
  "total": "integer",
  "total_currency_format": "string",
  "records": [
    {
      "id": "integer",
      "transaction_id": "integer",
      "amount": "string",
      "description": "string",
      "transaction_type_id": "integer",
      "transaction_type": "string",
      "transaction_no": "string",
      "amount_currency_format": "string",
      "transaction_due_date": {"type": "string","format": "date-time"},
      "transaction_total": "integer",
      "transaction_total_currency_format": "string",
      "transaction_balance_due": "integer",
      "transaction_balance_due_currency_format": "string"
    }
  ],
  "is_reconciled": "boolean",
  "is_create_before_conversion": "boolean",
  "is_import": "boolean",
  "import_id": "integer",
  "attachments": "array",
  "tags": "array",
  "tags_string": "",
  "created_at": {"type": "string","format": "date-time"},
  "updated_at": {"type": "string","format": "date-time"},
  "currency_code": "IDR",
  "currency_list_id": "integer",
  "currency_from_id": "integer",
  "currency_to_id": "integer",
  "multi_currency_id": "integer",
  "currency_rate": "integer",
  "comments_size": "integer"
}
```

## Example Response
{: .fw-300 }

```json
{
    "id": 4455095,
    "transaction_no": "10346",
    "token": "-bAyCSXEt3tkC2gtQEhpPw",
    "memo": "",
    "source": null,
    "custom_id": null,
    "status": "approved",
    "transaction_status": {
      "id": 3,
      "name": "Paid",
      "created_at": "2014-11-09T05:44:30.000Z",
      "updated_at": "2014-11-09T05:44:30.000Z",
      "name_bahasa": "Lunas"
    },
    "deleted_at": null,
    "audited_by": null,
    "transaction_date": "30/01/2024",
    "due_date": null,
    "person": {
      "id": 798833,
      "name": "Awan",
      "email": "rosa@gmail.com",
      "address": null,
      "phone": null,
      "fax": null
    },
    "transaction_type": {
      "id": 2,
      "name": "Receive Payment"
    },
    "payment_method": {
      "id": 1193180,
      "name": "Cash"
    },
    "deposit_to": {
      "id": 30918104,
      "name": "Cash",
      "number": "1-10001",
      "category": {
        "id": 3,
        "name": "Cash & Bank"
      }
    },
    "is_draft": false,
    "proforma_id": 2886,
    "witholding": {
      "witholding_account_name": null,
      "witholding_account_number": null,
      "account_id": null,
      "value": "0.0",
      "type": "value",
      "amount": 0,
      "amount_currency_format": "Rp.  0,00",
      "category": {
        "id": null,
        "name": null
      }
    },
    "original_amount": 10000,
    "original_amount_currency_format": "Rp.  10.000,00",
    "total": 10000,
    "total_currency_format": "Rp.  10.000,00",
    "records": [
      {
        "id": 1023667,
        "transaction_id": 4455094,
        "amount": "10000.0",
        "description": "",
        "transaction_type_id": 1,
        "transaction_type": "Sales Invoice",
        "transaction_no": "10242",
        "amount_currency_format": "Rp.  10.000,00",
        "transaction_due_date": "14/02/2024",
        "transaction_total": 10000,
        "transaction_total_currency_format": "Rp.  10.000,00",
        "transaction_balance_due": 10000,
        "transaction_balance_due_currency_format": "Rp.  10.000,00"
      }
    ],
    "is_reconciled": false,
    "is_create_before_conversion": null,
    "is_import": false,
    "import_id": null,
    "attachments": [],
    "tags": null,
    "tags_string": "",
    "created_at": "2024-01-30T11:17:53.000Z",
    "updated_at": "2024-01-30T11:17:53.000Z",
    "currency_code": "IDR",
    "currency_list_id": 8438,
    "currency_from_id": 1,
    "currency_to_id": 1,
    "multi_currency_id": 133378,
    "currency_rate": 1,
    "comments_size": 0
}
```