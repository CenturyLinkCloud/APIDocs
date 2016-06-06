{{{
  "title": "Create a Site to Site VPN",
  "date": "5-8-2016",
  "author": "Anthony Hakim",
  "attachments": [],
  "contentIsHTML": false
}}}

Creates a Site to Site VPN for a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you need to create a Site to Site VPN for a given account.

## URL

### Structure

    POST https://api.ctl.io/v2/siteToSiteVpn?account={accountId}

### Example

    POST https://api.ctl.io/v2/siteToSiteVpn?account=ACCT

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountId | string | Short code for a particular account | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| local | string |  | Yes |
| remote | string |  | Yes |
| ike | string |  | Yes |
| ipsec | string |  | Yes |

### Local Entity

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| locationAlias | string | Short code for a particular location | Yes |
| subnets | string | Local address for Site to Site VPN, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | Yes |

### Remote Entity

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| siteName | string | Friendly name of the site | Yes |
| deviceType | string | Friendly name of the device type | Yes |
| address | string | Remote address for Site to Site VPN, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | Yes |
| subnets | string | Remote network address for Site to Site VPN, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | Yes |

### IKE Entity

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| encryption | string |  | Yes |
| hashing | string |  | Yes |
| diffieHelmanGroup | string |  | Yes |
| preSharedKey | string |  | Yes |
| lifetime | string |  | Yes |
| mode | string |  | Yes |
| deadPeerDetection | string |  | Yes |
| natTraversal | string |  | Yes |
| remoteIdentity | string |  | Yes |

### IPSec Entity

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| encryption | string |  | Yes |
| hashing | string |  | Yes |
| protocol | string |  | Yes |
| pfs | string |  | Yes |
| lifetime | string |  | Yes |

### Example

#### JSON
```json
{
  "local": {
    "locationAlias": "WA1",            	  
    "subnets": [                          
      "10.10.10.0/24"
    ]
  },
  "remote": {
    "siteName": "API test",                
    "deviceType": "SRX and stuff",        
    "address": "1.1.1.1",
    "subnets": [                          
      "10.1.1.0/24"
    ]
  },
  "ike": {
    "encryption": "aes128",               
    "hashing": "sha1_96",                 
    "diffieHelmanGroup": "group2",        
    "preSharedKey": "Password123",
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
  }
}
```

## Response

The response will be an entity representing the new Site to Site VPN that was created.

### Example

#### JSON
```json

```
