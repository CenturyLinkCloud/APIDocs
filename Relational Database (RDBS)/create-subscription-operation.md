{{{
  "title": "Create Subscription Operation",
  "date": "04-09-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Initiate a subscription's operation. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to failover a replicated subscription. Subscription failover is an asynchronous process; valid requests will be accepted and the failover request queued for further processing.

## URL

### Structure

    POST https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}/operations

### Example

    POST https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744/operations

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account. | Yes |
| subscriptionId | number | Subscription id. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| type | string | 'failover' | Yes |

