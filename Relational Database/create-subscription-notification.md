{{{
  "title": "Create Subscription Notification",
  "date": "04-13-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Create a subscription notification. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a subscription's notification. Subscriptions can be configured to notify users of high CPU or Storage use through `Notifications`. When a new notification is created, the recipient must validate their email through a url provided in a notification verification email before they begin to receive email notifications.

## URL

### Structure

    POST https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}/notifications

### Example

    POST https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744/notifications

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account. | Yes |
| subscriptionId | number | Subscription id. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| destinationType | string | `EMAIL`. | Yes |
| recipient | string | Email address to send notificaitons to. | Yes |
| notificationTypes | array | One of more of CPU\_UTILIZATION, STORAGE\_UTILIZATION. | Yes |


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
