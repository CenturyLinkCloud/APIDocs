{{{
  "title": "Delete Subscription",
  "date": "04-10-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Delete an existing subscription. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete a subscription.

## URL

### Structure

    DELETE https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}

### Example

    DELETE https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| subscriptionId | number | Subscription id | Yes |


