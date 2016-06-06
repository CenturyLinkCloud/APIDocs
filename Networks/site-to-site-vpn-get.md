{{{
  "title": "Get Site to Site VPNs",
  "date": "6-8-2016",
  "author": "Anthony Hakim",
  "attachments": [],
  "contentIsHTML": false
}}}

Gets all Site to Site VPNs for a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you need to get a list Site to Site VPNs for a given account.

## URL

### Structure

    GET https://api.ctl.io/v2/siteToSiteVpn?account={accountId}

### Example

    GET https://api.ctl.io/v2/siteToSiteVpn?account=ACCT

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountId | string | Short code for a particular account | Yes |

## Response

The response will be an entity representing the Site to Site VPNs for a given account.

### Example

#### JSON
```json

```
