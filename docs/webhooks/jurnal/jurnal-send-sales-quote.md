---
layout: page
title: Send Sales Quote
permalink: /webhooks/jurnal/send-sales-quote
parent: Jurnal
grand_parent: Webhooks
---

# Send Sales Quote to Webhook Consumer Every New Sales Quote Created

## Prequisite to Consume
{: .fw-300 }
1. Feature sales quote webhook for that company is active in [Jurnal](https://jurnal.id)
2. User need to create new sales quote

## Event
{: .fw-300 }
```
jurnal.salesquote.created
```

## Schema
{: .fw-300 }

```json
{
        "kind": "string",
        "id": "integer",
        "transaction_no": "string",
        "email": "string",
        "address": "string",
        "message": "string",
        "memo": "string",
        "remaining": "string",
        "original_amount": "string",
        "discount_price": "string",
        "shipping_price": "string",
        "shipping_address": "string",
        "is_shipped": "boolean",
        "ship_via": "string",
        "subtotal": "string",
        "reference_no": "string",
        "tracking_no": "string",
        "tax_after_discount": "boolean",
        "discount_unit": "string",
        "tax_amount": "string",
        "status": "string",
        "custom_id": "string",
        "created_at": {"type": "string","format": "date-time"},
        "deleted_at": {"type": "string","format": "date-time"},
        "deletable": "boolean",
        "editable": "boolean",
        "audited_by": "string",
        "transaction_date": {"type": "string","format": "date"},
        "expiry_date": {"type": "string","format": "date"},
        "shipping_date": {"type": "string","format": "date"},
        "remaining_currency_format": "string",
        "shipping_price_currency_format": "string",
        "tax_amount_currency_format": "string",
        "discount_price_currency_format": "string",
        "subtotal_currency_format": "string",
        "discount_per_lines": "string",
        "discount_per_lines_currency_format": "string",
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
        "person": {
            "id": "integer",
            "display_name": "Adam",
            "email": "string",
            "address": "string",
            "phone": "string",
            "fax": "string"
        },
        "discount_type": {
            "id": "integer",
            "name": "string",
            "name_bahasa": "string"
        },
        "term": {
            "id": "integer",
            "name": "string",
            "longetivity": "integer"
        },
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
        "tags_string": "string",
        "updated_at": {"type": "string","format": "date-time"},
        "currency_code": "string",
        "disable_link": "boolean"
}
```

## Example Response
{: .fw-300 }

```json
{
        "kind": "Sales Quote",
        "id": 15192,
        "transaction_no": "10004",
        "email": "email@budi.com",
        "address": "Jalan Pengiriman X, Jakarta",
        "message": "message note",
        "memo": "memo note",
        "remaining": "3291624.0",
        "original_amount": "3291624.0",
        "discount_price": "64800.0",
        "shipping_price": "0.0",
        "shipping_address": null,
        "is_shipped": false,
        "ship_via": null,
        "subtotal": "3600000.0",
        "reference_no": "customer_100",
        "tracking_no": null,
        "tax_after_discount": true,
        "discount_unit": "2.0",
        "tax_amount": "116424.0",
        "status": "approved",
        "custom_id": null,
        "created_at": "2023-11-07T08:09:45.647Z",
        "deleted_at": null,
        "deletable": true,
        "editable": true,
        "audited_by": null,
        "transaction_date": "07/11/2023",
        "expiry_date": "07/12/2023",
        "shipping_date": null,
        "remaining_currency_format": "Rp.  3.291.624,00",
        "shipping_price_currency_format": "Rp.  0,00",
        "tax_amount_currency_format": "Rp.  116.424,00",
        "discount_price_currency_format": "Rp.  64.800,00",
        "subtotal_currency_format": "Rp.  3.600.000,00",
        "discount_per_lines": "360000.0",
        "discount_per_lines_currency_format": "Rp.  360.000,00",
        "transaction_status": {
            "id": 1,
            "name": "Open",
            "name_bahasa": "Belum Dibayar"
        },
        "transaction_lines_attributes": [
            {
                "id": 15181,
                "custom_id": null,
                "description": "Desc Mac",
                "amount": "1080000.0",
                "discount": "10.0",
                "rate": "1200000.0",
                "tax": null,
                "line_tax": {
                    "id": 1,
                    "name": "PPN",
                    "rate": "11.0",
                    "children": []
                },
                "amount_currency_format": "Rp.  1.080.000,00",
                "rate_currency_format": "Rp.  1.200.000,00",
                "has_return_line": false,
                "quantity": 1.0,
                "sell_acc_id": 148,
                "buy_acc_id": 150,
                "product": {
                    "id": 2,
                    "name": "Macbook 1",
                    "code": "",
                    "product_custom_id": null,
                    "archive": false,
                    "quantity": 0.0,
                    "quantity_string": "0.0",
                    "track_inventory": false,
                    "sell_price_per_unit": "1200000.0",
                    "buy_price_per_unit": "1000000.0",
                    "link": "http://localhost:3000/products/2"
                },
                "unit": {
                    "id": 1,
                    "name": "Pcs"
                },
                "units": [],
                "pricing_rule": null
            }
        ],
        "person": {
            "id": 5,
            "display_name": "Adam",
            "email": "",
            "address": null,
            "phone": null,
            "fax": null
        },
        "discount_type": {
            "id": 1,
            "name": "Percent",
            "name_bahasa": "Persen"
        },
        "term": {
            "id": 1,
            "name": "Net 30",
            "longetivity": 30
        },
        "tax": {
            "id": null,
            "name": null,
            "rate": null
        },
        "tax_details": [
            {
                "name": "PPN 11.0%",
                "tax_amount": 116424.0,
                "tax_amount_currency_format": "Rp.  116.424,00"
            }
        ],
        "use_tax_inclusive": false,
        "tags": [
            {
                "id": 6,
                "name": "tags one"
            },
            {
                "id": 7,
                "name": "tags two"
            }
        ],
        "tags_string": "tags one, tags two",
        "updated_at": "2023-11-07T08:09:45.647Z",
        "currency_code": "IDR",
        "disable_link": false
}
```