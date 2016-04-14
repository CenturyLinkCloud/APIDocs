{{{
  "title": "Get Subscription Notifications",
  "date": "04-13-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Returns all subscription notifications. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to see a subscription's notifications.

## URL

### Structure

    GET https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}/notifications

### Example

    GET https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744/notifications

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account. | Yes |
| subscriptionId | number | Subscription id. | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | number | Notification id. |
| destinationType | string | `EMAIL` |
| recipient | string | Email address the notification is delivered to. |
| notificationTypes | array | One of more of CPU\_UTILIZATION, STORAGE\_UTILIZATION. |
| verified | boolean | True if the recipient has verified their email address through the notification verification email. |


#### JSON

```json
[
  {
    "id": 19,
    "destinationType": "EMAIL",
    "recipient": "wilfred@example.com",
    "notificationTypes": [
      "CPU_UTILIZATION",
      "STORAGE_UTILIZATION"
    ],
    "verified": false
  }
]```
