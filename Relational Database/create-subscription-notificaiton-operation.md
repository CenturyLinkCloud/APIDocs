{{{
  "title": "Create Subscription Notification Operation",
  "date": "04-13-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Initiate a subscription notification's operation. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to verify a subscription notification. You must provide the token sent in the notification verification email.

## URL

### Structure

    POST https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}/notifications/{notificationId}/operations

### Example

    POST https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744/notifications/19/operations

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
| type | string | 'verify' | Yes |
| token | string | Token included in the notification verification email. | Yes |

