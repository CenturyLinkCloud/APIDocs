{{{
  "title": "Get Details for a Site to Site VPN",
  "date": "6-8-2016",
  "author": "Anthony Hakim",
  "attachments": [],
  "contentIsHTML": false
}}}

Gets Details for a Site to Site VPN for a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you need to get details for a Site to Site VPN for a given account.

## URL

### Structure

    GET https://api.ctl.io/v2/siteToSiteVpn/{vpnId}?account={accountId}

### Example

    GET https://api.ctl.io/v2/siteToSiteVpn/9c00bddea921670344d781378a8df615?account=ACCT

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountId | string | Short code for a particular account | Yes |
| vpnId | string | ID of the VPN | Yes |

## Response

The response will be an entity representing the details for a Site to Site VPN for a given account.

### Example

#### JSON
```json

```
