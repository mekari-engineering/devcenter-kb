---
layout: page
title: Send Sales Invoice
permalink: /webhooks/jurnal/send-sales-invoice
parent: Jurnal
grand_parent: Webhooks
---

# Send Sales Invoice to Webhook Consumer Every New Sales Invoice Created

## Prequisite to Consume
{: .fw-300 }
1. Feature sales invoice webhook for that company is active in Jurnal
2. User need to create new sales invoice

## Event
{: .fw-300 }
```
jurnal.salesinvoice.created
```

## Schema
{: .fw-300 }

```json
{
  "kind": "string",
  "id": "integer",
  "transaction_no": "string",
  "selected_po_id": "integer",
  "selected_pq_id": "integer",
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
  "witholding_value": "string",
  "status": "string",
  "discount_price": "string",
  "witholding_type": "string",
  "amount_receive": "string",
  "subtotal": "string",
  "deposit": "string",
  "custom_id": "string",
  "created_at": {"type": "string","format": "date-time"},
  "deleted_at": {"type": "string","format": "date-time"},,
  "audited_by": "string",
  "transaction_date": {"type": "string","format": "date-time"},
  "due_date": {"type": "string","format": "date-time"},
  "shipping_date": {"type": "string","format": "date"},
  "witholding_amount": "integer",
  "witholding_amount_currency_format": "string",
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
      "pricing_rule": "array"
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
    "fax": "string"
  },
  "discount_type": {
    "id": "integer",
    "name": "string",
    "name_bahasa": "string"
  },
  "discount_unit": "string",
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
  "witholding_account": {
    "id": "integer",
    "name": "string",
    "number": "integer",
    "category": {
      "id": "integer",
      "name": "string"
    }
  },
  "updated_at": {"type": "string","format": "date-time"},
  "currency_code": "IDR",
  "currency_list_id": "integer",
  "currency_from_id": "integer",
  "currency_to_id": "integer",
  "multi_currency_id": "integer",
  "currency_rate": "integer",
  "sales_withholdings": "array"
}
```

## Example Response
{: .fw-300 }

```json
{
    "kind": "Sales Invoice",
    "id": 4455096,
    "transaction_no": "10243",
    "selected_po_id": null,
    "selected_pq_id": null,
    "token": "ZzXVK1zgE3kEE7VF5MiCPA",
    "email": "morgan@gmail.com, fadzil@gmail.com",
    "source": "v3/revamp",
    "address": "Jl. jalan ke sumedank",
    "message": "Test Default msg",
    "memo": "",
    "remaining": "10000.0",
    "original_amount": "10000.0",
    "shipping_price": "0.0",
    "shipping_address": null,
    "is_shipped": false,
    "ship_via": "",
    "reference_no": "",
    "tracking_no": "",
    "tax_after_discount": true,
    "tax_amount": "0.0",
    "witholding_value": "0.0",
    "status": "approved",
    "discount_price": "0.0",
    "witholding_type": "value",
    "amount_receive": "0.0",
    "subtotal": "10000.0",
    "deposit": "0.0",
    "custom_id": null,
    "created_at": "2024-01-30T11:18:28.000Z",
    "deleted_at": null,
    "audited_by": null,
    "transaction_date": "30/01/2024",
    "due_date": "30/03/2024",
    "shipping_date": null,
    "witholding_amount": 0,
    "witholding_amount_currency_format": "Rp.  0,00",
    "discount_per_lines": "0.0",
    "discount_per_lines_currency_format": "Rp.  0,00",
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
    "has_deliveries": false,
    "is_create_before_conversion": null,
    "is_import": false,
    "import_id": null,
    "has_credit_memos": false,
    "credit_memo_balance": 0,
    "credit_memo_balance_currency_format": "Rp.  0,00",
    "transaction_status": {
      "id": 1,
      "name": "Open",
      "name_bahasa": "Belum Dibayar"
    },
    "transaction_lines_attributes": [
      {
        "id": 4670184,
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
        "pricing_rule": null
      }
    ],
    "payments": [],
    "sales_returns": [],
    "sales_deliveries": [],
    "credit_memos": [],
    "sales_quote": {
      "id": null,
      "transaction_no": null
    },
    "person": {
      "id": 717245,
      "display_name": "alicloudSRS",
      "title": null,
      "first_name": "",
      "middle_name": "",
      "last_name": "",
      "tax_no": "",
      "email": "morgan@gmail.com, fadzil@gmail.com",
      "address": "Jl. jalan ke Dufan",
      "billing_address": "Jl. jalan ke sumedank",
      "phone": "0895355293048",
      "fax": ""
    },
    "discount_type": {
      "id": 1,
      "name": "Percent",
      "name_bahasa": "Persen"
    },
    "discount_unit": "0.0",
    "warehouse": {
      "id": null,
      "name": null,
      "code": null,
      "status": null
    },
    "deposit_to": {
      "id": null,
      "name": null,
      "number": null,
      "category": {
        "id": null,
        "name": null
      }
    },
    "term": {
      "id": 296675,
      "name": "Net 60",
      "longetivity": 60
    },
    "tags": null,
    "tags_string": "",
    "has_payments": false,
    "earliest_payment_date": "",
    "tax": {
      "id": null,
      "name": null,
      "rate": null
    },
    "tax_details": [],
    "use_tax_inclusive": false,
    "attachments": [],
    "email_previews": {
      "times_sent": 0,
      "sent_to_list": []
    },
    "is_reconciled": false,
    "witholding_account": {
      "id": null,
      "name": null,
      "number": null,
      "category": {
        "id": null,
        "name": null
      }
    },
    "updated_at": "2024-01-30T11:18:28.000Z",
    "currency_code": "IDR",
    "currency_list_id": 8438,
    "currency_from_id": 1,
    "currency_to_id": 1,
    "multi_currency_id": 133379,
    "currency_rate": 1,
    "sales_withholdings": []
}
```