{{{
  "title": "Get Billing",
  "date": "04-02-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Returns current RDBS billing for an entire account or individual subscription. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to see current billing for the entire account or a single subscription.

## URL

### Structure

    GET https://api.rdbs.ctl.io/v1/{accountAlias}/billing?subscriptionId={subscriptionId}

### Example

    GET https://api.rdbs.ctl.io/v1/ALIAS/billing?subscriptionId=744

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

### Query Parameters

| Name | Type | Description |
| --- | --- | --- |
| subscriptionId | number | Subscription id to narrow billing focus to a single subscription. You can get a list of all subscriptions with [Get Subscriptions](get-subscriptions.md) API operation.|


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| productCode | **_future_** | **_future_** |
| metadata | object | **_future_** |
| monthlyEstimate | string | Estimate of monthly charge for this account or subscription. |
| monthToDate | string | Monthly charges to date for this account or subscription. |
| currentHour | string | Hourly charges for this account or subscription. |

#### JSON

```json
{
  "productCode": null,
  "metadata": {},
  "monthlyEstimate": "$446.83",
  "monthToDate": "$85.52",
  "currentHour": "$0.60"
}
```
