{{{
  "title": "Get Subscription Certificate",
  "date": "04-13-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Returns the subscription TLS certificate as a stream. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to download a subscription certificate. Subscription certificates are included in the [Get Subscription](get-subscription.md) API operation; this API operation downloads the certificate as a file. 

## URL

### Structure

    GET https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}/certificate

### Example

    GET https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744/certificate

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
| N/A | octet stream | The certificate is returned as `application/octet-stream` with a default name of `<subscription.externalId>.pem`|

