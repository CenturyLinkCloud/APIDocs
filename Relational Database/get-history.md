{{{
  "title": "Get History",
  "date": "04-05-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Returns an ordered history of actions performed on all account subscriptions, or a single subscription. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to see actions performed on all subscriptions on an account, or actions performed on a single subscription.

## URL

### Structure

    GET https://api.rdbs.ctl.io/v1/{accountAlias}/history?subscriptionId={subscriptionId}

### Example

    GET https://api.rdbs.ctl.io/v1/ALIAS/history
    GET https://api.rdbs.ctl.io/v1/ALIAS/history?subscriptionId=744

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account. | Yes |

### Query Parameters

| Name | Type | Description |
| --- | --- | --- |
| subscriptionId | number | Subscription id to narrow focus to a single subscription. Subscription Ids are listed in the [Get Subscriptions](get-subscriptions.md) API operation.|


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| timestamp | number | Unix style timestamp; milliseconds since epoch. |
| message | string | Summary message of form "subscription name: message". |
| details | string | Additional details, if available. |
| user | string | User initiating the action. An RDBS service account is listed when the action is provided by the service, like automated failover to replicated instances. |

#### JSON

```json
[
  {
    "timestamp": 1459878501968,
    "message": "demo-dev: created.",
    "details": "1 CPU, 1GB RAM, 1GB storage",
    "user": "user1"
  },
  {
    "timestamp": 1459878122697,
    "message": "poc1-test: deleted.",
    "details": null,
    "user": "user2"
  },
  {
    "timestamp": 1459455272384,
    "message": "config-db: failed over (automatic).",
    "details": "Primary server became active.",
    "user": "dbaas_service"
  },
  ...
]
```
