{{{
  "title": "Update Subscription Notification",
  "date": "04-18-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Update a subscription notification. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change a subscription notification. 

## URL

### Structure

    PUT https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}/notifications/{notificationId}

### Example

    PUT https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744/notifications/19

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account. | Yes |
| subscriptionId | number | Subscription id. | Yes |
| notificationId | number | Notification id. | Yes |

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
