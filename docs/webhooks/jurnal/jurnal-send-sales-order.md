---
layout: page
title: Send Sales Order
permalink: /webhooks/jurnal/send-sales-order
parent: Jurnal
grand_parent: Webhooks
---

# Send Sales Order to Webhook Consumer Every New Sales Order Created

## Prequisite to Consume
{: .fw-300 }
1. Feature sales order webhook for that company is active in Jurnal
2. User need to create new sales order

## Event
{: .fw-300 }
```
jurnal.salesorder.created
```

## Schema
{: .fw-300 }

```json
{
  "kind": "string",
  "id": "integer",
  "transaction_no": "string",
  "selected_po_id": "integer",
  "token": "string",
  "email": "string",
  "source": "string",
  "address": "string",
  "message": "string",
  "memo": "string",
  "remaining": "string",
  "original_amount": "string",
  "shipping_price": "string",
  "shipping_address": "string",
  "is_shipped": "boolean",
  "ship_via": "string",
  "reference_no": "string",
  "tracking_no": "string",
  "tax_after_discount": "boolean",
  "tax_amount": "string",
  "status": "string",
  "discount_price": "string",
  "amount_receive": "string",
  "subtotal": "string",
  "deposit": "string",
  "custom_id": "string",
  "created_at": {"type": "string","format": "date-time"},
  "deleted_at": {"type": "string","format": "date-time"},,
  "transaction_date": {"type": "string","format": "date-time"},
  "due_date": {"type": "string","format": "date-time"},
  "shipping_date": {"type": "string","format": "date"},
  "discount_per_lines": "string",
  "discount_per_lines_currency_format": "string",
  "payment_received_amount": "string",
  "payment_received_amount_currency_format": "string",
  "remaining_currency_format": "string",
  "original_amount_currency_format": "string",
  "shipping_price_currency_format": "string",
  "tax_amount_currency_format": "string",
  "discount_price_currency_format": "string",
  "amount_receive_currency_format": "string",
  "subtotal_currency_format": "string",
  "deposit_currency_format": "string",
  "has_deliveries": "boolean",
  "is_create_before_conversion": "boolean",
  "is_import": "boolean",
  "import_id": "integer",
  "has_credit_memos": "boolean",
  "credit_memo_balance": "integer",
  "credit_memo_balance_currency_format": "string",
  "transaction_status": {
    "id": "integer",
    "name": "string",
    "name_bahasa": "string"
  },
  "transaction_lines_attributes": [
    {
      "id": "integer",
      "custom_id": "string",
      "description": "string",
      "amount": "string",
      "discount": "string",
      "rate": "string",
      "tax": "string",
      "line_tax": {
        "id": "integer",
        "name": "string",
        "rate": "string",
        "children": "array"
      },
      "amount_currency_format": "string",
      "rate_currency_format": "string",
      "has_return_line": "boolean",
      "quantity": "double",
      "sell_acc_id": "integer",
      "buy_acc_id": "integer",
      "product": {
        "id": "integer",
        "name": "string",
        "code": "string",
        "product_custom_id": "string",
        "archive": "boolean",
        "quantity": "double",
        "quantity_string": "string",
        "track_inventory": "boolean",
        "sell_price_per_unit": "string",
        "buy_price_per_unit": "string",
        "link": "string"
      },
      "unit": {
        "id": "integer",
        "name": "string"
      },
      "units": "array",
      "pricing_rule": "array",
      "remaining_quantity": "integer"
    }
  ],
  "payments": "array",
  "sales_returns": "array",
  "sales_deliveries": "array",
  "credit_memos": "array",
  "sales_quote": {
    "id": "integer",
    "transaction_no": "string"
  },
  "deliveries": "array",
  "payment_transactions": "array",
  "invoices": "array",
  "person": {
    "id": "integer",
    "display_name": "string",
    "title": "string",
    "first_name": "string",
    "middle_name": "string",
    "last_name": "string",
    "tax_no": "string",
    "email": "string",
    "address": "string",
    "billing_address": "string",
    "phone": "string",
    "fax": "string",
    "mobile": "string",
    "tax_no": "string"
  },
  "discount_type": {
    "id": "integer",
    "name": "string",
    "name_bahasa": "string"
  },
  "warehouse": {
    "id": "integer",
    "name": "string",
    "code": "string",
    "status": "string"
  },
  "deposit_to": {
    "id": "integer",
    "name": "string",
    "number": "integer",
    "category": {
      "id": "integer",
      "name": "string"
    }
  },
  "term": {
    "id": "integer",
    "name": "string",
    "longetivity": "integer"
  },
  "tags": [
    {
      "id": "integer",
      "name": "string"
    },
    {
      "id": "integer",
      "name": "string"
    }
  ],
  "tags_string":"string",
  "has_payments": "boolean",
  "earliest_payment_date": {"type": "string","format": "date-time"},
  "tax": {
    "id": "integer",
    "name": "string",
    "rate": "string"
  },
  "tax_details": [
    {
      "name": "string",
      "tax_amount": "double",
      "tax_amount_currency_format": "string"
    }
  ],
  "use_tax_inclusive": "boolean",
  "attachments": "array",
  "email_previews": {
    "times_sent": "integer",
    "sent_to_list": "array"
  },
  "is_reconciled": "boolean",
  "updated_at": {"type": "string","format": "date-time"},
  "currency_code": "IDR",
  "currency_list_id": "integer",
  "currency_from_id": "integer",
  "currency_to_id": "integer",
  "multi_currency_id": "integer",
  "currency_rate": "integer",
  "company_currency": {
    "code": "string",
    "symbol": "string"
  }
}
```

## Example Response
{: .fw-300 }

```json
{
    "kind": "Sales Order",
    "id": 4455088,
    "transaction_no": "10111",
    "token": "XY8xDfKNrximmSNQtOmh5Q",
    "email": "morgan@gmail.com, fadzil@gmail.com",
    "source": "v3/revamp",
    "address": "Jl. jalan ke sumedank",
    "message": "Test Default msg",
    "memo": "",
    "shipping_address": null,
    "is_shipped": false,
    "selected_po_id": null,
    "ship_via": "",
    "reference_no": "",
    "tracking_no": "",
    "status": "approved",
    "custom_id": null,
    "created_at": "2024-01-30T11:10:45.000Z",
    "deleted_at": null,
    "transaction_date": "30/01/2024",
    "due_date": "30/03/2024",
    "shipping_date": null,
    "original_amount": "10000.0",
    "remaining": "10000.0",
    "discount_unit": "0.0",
    "discount_price": "0.0",
    "shipping_price": "0.0",
    "amount_receive": "0.0",
    "tax_after_discount": true,
    "tax_amount": "0.0",
    "subtotal": "10000.0",
    "deposit": "0.0",
    "payment_received_amount": "0.0",
    "payment_received_amount_currency_format": "Rp.  0,00",
    "remaining_currency_format": "Rp.  10.000,00",
    "original_amount_currency_format": "Rp.  10.000,00",
    "shipping_price_currency_format": "Rp.  0,00",
    "tax_amount_currency_format": "Rp.  0,00",
    "discount_price_currency_format": "Rp.  0,00",
    "amount_receive_currency_format": "Rp.  0,00",
    "subtotal_currency_format": "Rp.  10.000,00",
    "deposit_currency_format": "Rp.  0,00",
    "discount_per_lines": "0.0",
    "discount_per_lines_currency_format": "Rp.  0,00",
    "tax": {
      "id": null,
      "name": null,
      "rate": null
    },
    "tax_details": [],
    "use_tax_inclusive": false,
    "deposit_to": {
      "id": null,
      "name": null,
      "number": null,
      "category": {
        "id": null,
        "name": null
      }
    },
    "transaction_status": {
      "id": 1,
      "name": "Open",
      "name_bahasa": "Belum Dibayar"
    },
    "transaction_lines_attributes": [
      {
        "id": 4670179,
        "custom_id": null,
        "description": "",
        "amount": "10000.0",
        "discount": "0.0",
        "rate": "10000.0",
        "tax": null,
        "line_tax": {
          "id": null,
          "name": null,
          "rate": null,
          "children": []
        },
        "amount_currency_format": "Rp.  10.000,00",
        "rate_currency_format": "Rp.  10.000,00",
        "has_return_line": false,
        "quantity": 1,
        "sell_acc_id": 30918337,
        "buy_acc_id": 30918340,
        "product": {
          "id": 14523140,
          "name": "A1 Morgan Ganteng",
          "code": null,
          "product_custom_id": null,
          "archive": false,
          "quantity": 0,
          "quantity_string": "0.0",
          "track_inventory": false,
          "sell_price_per_unit": "10000.0",
          "buy_price_per_unit": "0.0",
          "link": null
        },
        "unit": {
          "id": 83000,
          "name": "Buah"
        },
        "units": [],
        "pricing_rule": null,
        "remaining_quantity": 1
      }
    ],
    "person": {
      "id": 717245,
      "title": null,
      "first_name": "",
      "middle_name": "",
      "last_name": "",
      "display_name": "alicloudSRS",
      "email": "morgan@gmail.com, fadzil@gmail.com",
      "address": "Jl. jalan ke Dufan",
      "billing_address": "Jl. jalan ke sumedank",
      "phone": "0895355293048",
      "fax": "",
      "mobile": "",
      "tax_no": ""
    },
    "discount_type": {
      "id": 1,
      "name": "Percent",
      "name_bahasa": "Persen"
    },
    "warehouse": {
      "id": null,
      "name": null,
      "code": null,
      "status": null
    },
    "sales_quote": {
      "id": null,
      "transaction_no": null
    },
    "tags": null,
    "tags_string": "",
    "term": {
      "id": 296675,
      "name": "Net 60",
      "longetivity": 60
    },
    "is_reconciled": false,
    "attachments": [],
    "payments": [],
    "deliveries": [],
    "payment_transactions": [],
    "invoices": [],
    "updated_at": "2024-01-30T11:10:45.000Z",
    "currency_code": "IDR",
    "currency_list_id": 8438,
    "currency_from_id": 1,
    "currency_to_id": 1,
    "multi_currency_id": 133371,
    "currency_rate": 1,
    "company_currency": {
      "code": "IDR",
      "symbol": "Rp."
    }
}
```