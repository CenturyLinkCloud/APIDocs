{{{
  "title": "Create Subscription Backup",
  "date": "04-13-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Create a subscription backup. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to initiate a subscription backup. Backup creation is an asynchronous process; valid requests will be accepted and the create request queued for further processing.

## URL

### Structure

    POST https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}/backups

### Example

    POST https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744/backups

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account. | Yes |
| subscriptionId | number | Subscription id. | Yes |

