{{{
  "title": "Get Promotions",
  "date": "04-13-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Returns all promotions applied to this account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to see all promotions applied to an account.

## URL

### Structure

    GET https://api.rdbs.ctl.io/v1/{accountAlias}/promotions
    
### Example

    GET https://api.rdbs.ctl.io/v1/ALIAS/promotions

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account. | Yes |


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| code | string | Promotion code. |

#### JSON

```json
{
  "code": "PROMO_2016"
}
```
