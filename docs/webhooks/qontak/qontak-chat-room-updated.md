---
layout: page
title: Edit Room
permalink: /webhooks/qontak/qontak-chat-room-updated
nav_order: 12
parent: Qontak
grand_parent: Webhooks
---

# Edit Room

## Prequisite to consume
{: .fw-300 }
1. webhook when there is changes on room status
  - assigned
  - resolved
1. webhook that triggered when there is changes inside room status

## Event
{: .fw-300 }
```
qontak.chat.room.updated
```

## Schema
{: .fw-300 }

```javascript
{
  "id": String,
  "name": String,
  "description": String,
  "status": String,
  "type": String,
  "tags": [],
  "channel": String,
  "channel_account": String,
  "organization_id": String,
  "account_uniq_id": String,
  "channel_integration_id": String,
  "session_at": Date,
  "last_message": {
    "id": String,
    "type": String,
    "room_id": String,
    "is_campaign": Boolean,
    "sender_id": String,
    "sender_type": String,
    "participant_id": String,
    "participant_type": String,
    "organization_id": String,
    "text": String,
    "status": String,
    "channel": String,
    "raw_message": {
      "contacts": [
        {
          "wa_id": String,
          "profile": {
            "name": String
          }
        }
      ],
      "messages": [
        {
          "id": String,
          "from": String,
          "text": {
            "body": String
          },
          "type": String,
          "timestamp": String
        }
      ],
      "metadata": {
        "phone_number_id": String,
        "display_phone_number": String
      },
      "messaging_product": String
    },
    "external_id": String,
    "local_id": null,
    "created_at": Date
  },
  "unread_count": Number,
  "created_at": String,
  "last_message_at": Date,
  "last_activity_at": Date,
  "updated_at": Date,
  "avatar": {
    "url": String,
    "large": {
      "url": String
    },
    "filename": null,
    "size": Number,
    "small": {
      "url": String
    },
    "medium": {
      "url": String
    }
  },
  "note": null,
  "resolved_at": null,
  "external_id": "",
  "resolved_by_id": null,
  "resolved_by_type": null,
  "extra": {
    "is_participant_online": Boolean
  },
  "agent_ids": [],
  "is_dont_auto_resolve": Boolean,
  "email_cc": null,
  "is_unresponded": Boolean,
  "is_manual_survey": Boolean,
  "data_event": String
}
```

## Example Response
{: .fw-300 }

```json
{
  "id": "5113b80b-fa7d-4a50-9590-1dfd55325580",
  "name": "adrian",
  "description": "",
  "status": "unassigned",
  "type": "Models::CustomerServiceRoom",
  "tags": [],
  "channel": "wa_cloud",
  "channel_account": "Sandbox Qontak 6",
  "organization_id": "859438e6-10ac-48ac-8d8c-d9d20bba8382",
  "account_uniq_id": "6282271511514",
  "channel_integration_id": "fa914ed7-672d-4530-97bd-1c554ab2e1ee",
  "session_at": "2024-05-15T16:36:04.000Z",
  "last_message": {
    "id": "a667db6f-6b67-4320-bfc2-b098f4ed2e2a",
    "type": "text",
    "room_id": "5113b80b-fa7d-4a50-9590-1dfd55325580",
    "is_campaign": false,
    "sender_id": "5f43e133-866c-4e5f-aaf1-3b92ccec0ee4",
    "sender_type": "Models::Contact",
    "participant_id": "1f345792-fe27-422c-9fa5-e54afe12d406",
    "participant_type": "customer",
    "organization_id": "859438e6-10ac-48ac-8d8c-d9d20bba8382",
    "text": "asdasd",
    "status": "created",
    "channel": "wa_cloud",
    "raw_message": {
      "contacts": [
        {
          "wa_id": "6282271511514",
          "profile": {
            "name": "Adrian Rahmandanu"
          }
        }
      ],
      "messages": [
        {
          "id": "wamid.HBgNNjI4MjI3MTUxMTUxNBUCABIYFDNBRjFBN0UxRUIyOTE2Q0IxRDg2AA==",
          "from": "6282271511514",
          "text": {
            "body": "asdasd"
          },
          "type": "text",
          "timestamp": "1715790964"
        }
      ],
      "metadata": {
        "phone_number_id": "540083594083559",
        "display_phone_number": "6289618625602"
      },
      "messaging_product": "whatsapp"
    },
    "external_id": "wamid.HBgNNjI4MjI3MTUxMTUxNBUCABIYFDNBRjFBN0UxRUIyOTE2Q0IxRDg2AA==",
    "local_id": null,
    "created_at": "2024-05-15T16:36:04.000Z"
  },
  "unread_count": 1,
  "created_at": "2024-05-15T16:36:05.675Z",
  "last_message_at": "2024-05-15T16:36:04.000Z",
  "last_activity_at": "2024-05-15T16:36:04.000Z",
  "updated_at": "2024-05-15T16:36:05.702Z",
  "avatar": {
    "url": "https://qontak-hub-production.s3-ap-southeast-1.amazonaws.com/assets/qi-user.png",
    "large": {
      "url": "https://qontak-hub-production.s3-ap-southeast-1.amazonaws.com/assets/qi-user.png"
    },
    "filename": null,
    "size": 0,
    "small": {
      "url": "https://qontak-hub-production.s3-ap-southeast-1.amazonaws.com/assets/qi-user.png"
    },
    "medium": {
      "url": "https://qontak-hub-production.s3-ap-southeast-1.amazonaws.com/assets/qi-user.png"
    }
  },
  "note": null,
  "resolved_at": null,
  "external_id": "",
  "resolved_by_id": null,
  "resolved_by_type": null,
  "extra": {
    "is_participant_online": false
  },
  "agent_ids": [],
  "is_dont_auto_resolve": false,
  "email_cc": null,
  "is_unresponded": true,
  "is_manual_survey": false,
  "data_event": "add_agent"
}
```