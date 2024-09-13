---
layout: page
title: Retrieve Output Tax Invoice PDF
permalink: /webhooks/klikpajak/klikpajak-efakturpdf-generated
parent: Klikpajak
grand_parent: Webhooks
---

# Retrieve Output Tax Invoice PDF

Notify users when PDF Link has been created

## Event
{: .fw-300 }
```
klikpajak.efakturpdf.generated
```

## Schema
{: .fw-300 }

```javascript
{
  "efakturOutPdfLink": String,
  "efakturOutId": Number
}
```

## Example Response
{: .fw-300 }

```json
{
  "efakturOutPdfLink": "https://jurnal-tax-efaktur-pdf-dev.s3.ap-southeast-1.amazonaws.com/243/2023/APRIL123113231223132-0110002300000002-123113231223132-20230406114753",
  "efakturOutId": 1824
}
```