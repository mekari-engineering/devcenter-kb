---
layout: default
title: Changelog
permalink: changelog
nav_order: 5
---

# Changelog

This changelog lists all additions and updates to the Mekari product API, in chronological order.

## December 12, 2023
{: .fw-300 }

Add support for query params if `request-line` header included on signature during HMAC Authentication process to enhance security protection during API authentication process. This means when generating the HMAC signature with `request-line` header, you need to add query params if the API URI has query param.

Previously if the full API URI is `POST https://api.mekari.com/v2/klikpajak/v1/efaktur/out?auto_approval=false`, the `request-line` will only contain method, path and http version. For example: `POST /v2/klikpajak/v1/efaktur/out HTTP/1.1`. However with this new changes, you must include the query params inside the `request-line`. For example: `POST /v2/klikpajak/v1/efaktur/out?auto_approval=false HTTP/1.1`.

Support for `request-line` without query params is deprecated and we will drop the support by March 31st, 2023. We expect you made the changes on your application before March 31st, 2023.

