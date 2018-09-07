{{{
  "title": "Delete a Site to Site VPN",
  "date": "6-14-2016",
  "author": "Anthony Hakim",
  "attachments": [],
  "contentIsHTML": false
}}}

Deletes a Site to Site VPN for a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you need to delete a Site to Site VPN for a given account.

## URL

### Structure

    DELETE https://api.ctl.io/v2/siteToSiteVpn/{vpnId}?account={accountId}

### Example

    DELETE https://api.ctl.io/v2/siteToSiteVpn/4FA8D6C83271CA53F9ABA815D7F4A0DD?account=ACCT

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountId | string | Short code for a particular account | Yes |
| vpnId | string | ID of the VPN | Yes |

## Response

The response will be the job ID in the Queue, for the Site to Site VPN that is to be deleted.

### Example

#### JSON
```json
"54851"
```
