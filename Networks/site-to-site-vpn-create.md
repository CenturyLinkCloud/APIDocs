{{{
  "title": "Create a Site to Site VPN",
  "date": "6-8-2016",
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

| Name | Type | Description | Option | Req. |
| --- | --- | --- | --- |
| encryption | string | Encryption Algorithm. | aes128, aes192, aes256, tripleDES | Yes |
| hashing | string | Hashing Algorithm. | sha1_96, sha1_256, md5 | Yes |
| diffieHelmanGroup | string | Group 1 (legacy), Group 2 or Group 5. If using AES with a cipher strength greater than 128-bit, or SHA2 for hashing, we recommend Group 5, otherwise Group 2 is sufficient. | group1, group2, group5 | Yes |
| preSharedKey | string | The pre-shared key is a shared secret that secures the VPN tunnel. This value must be identical on both ends of the connection. |  | Yes |
| lifetime | string | Lifetime is set to 8 hours for IKE. This is not required to match, as the negotiation will choose the shortest value supplied by either peer. |  | Yes |
| mode | string | Protocol Mode. | main, aggressive | Yes |
| deadPeerDetection | string | Dead-Peer Detection: Specify if you wish this enabled or disabled. Check your device defaults; for example, Cisco ASA defaults to 'on', while Netscreen/Juniper SSG or Juniper SRX default to 'off'. Our default is 'off'. | boolean | Yes |
| natTraversal | string | NAT-Traversal: Allows connections to VPN end-points behind a NAT device. Defaults to 'off'. If you require NAT-T, you also need to provide the private IP address that your VPN endpoint will use to identify itself. | boolean | Yes |
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
