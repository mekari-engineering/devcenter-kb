---
layout: default
title: Changelog
permalink: changelog
nav_order: 6
---
# Changelog

This changelog lists all additions and updates to the Mekari product API, in chronological order.

## Sep 18,2024

{: .fw-300 }

Java Documentation:
1. Add header ```Accept``` ```application/json```
2. Add header ```Content-Type``` ```application/json```
2. Declared JSON variable at Making API Request Section
3. Changed ```<maven.compiler.source>``` and ```<maven.compiler.target>``` to 1.8 since Java 8 is denoted as 1.8.
4. Corrected the missing closing tag ```</dependencies>```.

## Sep 13,2024

{: .fw-300 }

- Update header Accept application/json HMAC Authentication for Node.js documentation.
- Update header Accept application/json HMAC Authentication and add MEKARI_API_BASE_URL in .env file for PHP documentation.

## June 14,2024

{: .fw-300 }

Adding Platform, [Klikpajak](https://klikpajak.id), Qontak, [Jurnal](https://jurnal.id) and Talenta webhooks documentation.

## June 07,2024

{: .fw-300 }

Updating webhook events documentation.

## February 26,2024

{: .fw-300 }

Adding [jurnal](https://jurnal.id) api docs, mekari pay service, kyc-backend api documentation.


## February 22, 2024

{: .fw-300 }

Adding Updates for Product APIs documentation (Qontak CRM and Qontak OmniChannel)

## December 12, 2023

{: .fw-300 }

Add support for query params if `request-line` header included on signature during HMAC Authentication process to enhance security protection during API authentication process. This means when generating the HMAC signature with `request-line` header, you need to add query params if the API URI has query param.

Previously if the full API URI is `POST https://api.mekari.com/v2/klikpajak/v1/efaktur/out?auto_approval=false`, the `request-line` will only contain method, path and http version. For example: `POST /v2/klikpajak/v1/efaktur/out HTTP/1.1`. However with this new changes, you must include the query params inside the `request-line`. For example: `POST /v2/klikpajak/v1/efaktur/out?auto_approval=false HTTP/1.1`. If you need help to verify the implementation you can always use [HMAC Validator](https://developers.mekari.com/dashboard/hmac-validator) to verify your signature is correct or not.

Support for `request-line` without query params is deprecated and we will drop the support by March 31st, 2023. We expect you made the changes on your application before March 31st, 2023.
