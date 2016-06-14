{{{
  "title": "Get Details for a Site to Site VPN",
  "date": "6-14-2016",
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

    GET https://api.ctl.io/v2/siteToSiteVpn/4FA8D6C83271CA53F9ABA815D7F4A0DD?account=ACCT

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
{
    "id": "4FA8D6C83271CA53F9ABA815D7F4A0DD",
    "changeInfo": {
      "createdBy": "username",
      "createdDate": "2016-06-14T16:22:51Z",
      "modifiedBy": "username",
      "modifiedDate": "2016-06-14T17:53:12Z"
    },
    "accountAlias": "ACCT",
    "local": {
        "address": "4.3.2.1",
        "locationAlias": "WA1",
        "locationDescription": "WA1 - US West (Seattle)",
        "subnets": [
            "10.10.10.0/24"
        ]
    },
    "remote": {
        "siteName": "API test",
        "deviceType": "SRX and stuff",
        "address": "1.2.3.4",
        "subnets": [
            "10.1.1.0/24"
        ]
    },
    "ike": {
        "encryption": "aes128",
        "hashing": "sha1_96",
        "diffieHellmanGroup": "group2",
        "lifetime": 28800,
        "mode": "main",
        "deadPeerDetection": false,
        "natTraversal": false,
        "remoteIdentity": null
    },
    "ipsec": {
        "encryption": "aes128",
        "hashing": "sha1_96",
        "protocol": "esp",
        "pfs": "group2",
        "lifetime": 3600
    },
    "links": [
        {
            "rel": "self",
            "href": "/v2/siteToSiteVpn/4FA8D6C83271CA53F9ABA815D7F4A0DD?account=ACCT"
        }
    ]
}
```
