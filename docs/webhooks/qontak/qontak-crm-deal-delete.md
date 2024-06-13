---
layout: page
title: Delete Deals
permalink: /webhooks/qontak/qontak-crm-deal-delete
nav_order: 4
parent: Qontak
grand_parent: Webhooks
---

# Delete Deals

## Prequisite to consume
{: .fw-300 }
1. If client know ID of the deal, it can be delete by hit endpoint delete. or just delete the deal in UI
1. when Client delete the deal, we will inform client that deal with ID xx is successfully deleted.

## Event
{: .fw-300 }
```
qontak.crm.deal.delete
```

## Schema
{: .fw-300 }

```javascript
{
  "meta": {
    "status": Number,
    "type": String,
    "error_code": String, //null
    "info": "https://developers.qontak.com/docs/api/response-codes#200",
    "developer_message": String //// inform that data is succesfully deleted
    "message": String,
    "timestamp": Date,
    "log_id": String
  },
 "response" : {
  "id": Number, 
  "name": String,
  "slug": String,
  "external_company_id": Number,
  }
}
```

## Example Response
{: .fw-300 }

```json
{
  "meta": {
    "status": 200,
    "type": "OK",
    "error_code": null,
    "info": "https://developers.qontak.com/docs/api/response-codes#200",
    "developer_message": "Deal with id 9 successfully deleted",
    "message": "Success",
    "timestamp": "2021-07-20T00:00:00.000+07:00",
    "log_id": "a3aed8a9-5b69-42a0-8718-0015b70456bc"
  },
 "response" : {
  "id": 9, 
  "name": "Deal Astra Januari 2022",
  "slug": "88503b7f-289b-4edc-b185-51670b9cebff",
  "external_company_id":  12332
  }
}
```