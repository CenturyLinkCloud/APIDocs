{{{
  "title": "Update a Site to Site VPN",
  "date": "6-14-2016",
  "author": "Anthony Hakim",
  "attachments": [],
  "contentIsHTML": false
}}}

Updates a Site to Site VPN for a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you need to update a Site to Site VPN for a given account.

## URL

### Structure

    PUT https://api.ctl.io/v2/siteToSiteVpn/{vpnId}?account={accountId}

### Example

    PUT https://api.ctl.io/v2/siteToSiteVpn/4FA8D6C83271CA53F9ABA815D7F4A0DD?account=ACCT

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountId | string | Short code for a particular account | Yes |
| vpnId | string | ID of the VPN | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| local | string | Local site properties | No |
| remote | string | Remote site properties | No |
| ike | string | IKE properties | No |
| ipsec | string | IPSec properties | No |

### Local Entity

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| subnets | string | Local address for Site to Site VPN, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | No |

### Remote Entity

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| siteName | string | Friendly name of the site | No |
| deviceType | string | Friendly name of the device type | No |
| address | string | Remote address for Site to Site VPN, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | No |
| subnets | string | Remote network address for Site to Site VPN, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | No |

### IKE Entity

| Name | Type | Description | Option | Req. |
| --- | --- | --- | --- | --- |
| encryption | string | Encryption algorithm | aes128, aes192, aes256, tripleDES | No |
| hashing | string | Hashing algorithm | sha1_96, sha1_256, md5 | No |
| diffieHelmanGroup | string | Group 1 (legacy), Group 2 or Group 5. If using AES with a cipher strength greater than 128-bit, or SHA2 for hashing, we recommend Group 5, otherwise Group 2 is sufficient | group1, group2, group5 | No |
| preSharedKey | string | The pre-shared key is a shared secret that secures the VPN tunnel. This value must be identical on both ends of the connection |  | No |
| lifetime | string | Lifetime is set to 8 hours for IKE. This is not required to match, as the negotiation will choose the shortest value supplied by either peer | 3600, 28800, 86400 | No |
| mode | string | Protocol mode | main, aggressive | No |
| deadPeerDetection | boolean | Specify if you wish this enabled or disabled. Check your device defaults; for example, Cisco ASA defaults to 'on', while Netscreen/Juniper SSG or Juniper SRX default to 'off'. Our default is 'off'. | true/false | No |
| natTraversal | boolean | NAT-Traversal: Allows connections to VPN end-points behind a NAT device. Defaults to 'off'. If you require NAT-T, you also need to provide the private IP address that your VPN endpoint will use to identify itself. | true/false | No |
| remoteIdentity | string | The private IP address that your VPN endpoint will use to identify itself. Required only when NAT-T state is on | a valid IPv4 address | No |

### IPSec Entity

| Name | Type | Description | Option | Req. |
| --- | --- | --- | --- | --- |
| encryption | string | Encryption algorithm | aes128, aes192, aes256, tripleDES | No |
| hashing | string | Hashing algorithm | sha1_96, sha1_256, md5 | No |
| protocol | string | IPSec protocol | esp, ah | No |
| pfs | string | PFS enabled or disabled (we suggest enabled, using Group 2, though Group 5 is recommended with SHA2 hashing or AES-192 or AES-256) | disabled, group1, group2, group5 | No |
| lifetime | string | Lifetime is set to 1 hour (and unlimited KB). This setting is not required to match, as the negotiation process will choose the shortest value supplied by either peer. | 3600, 28800, 86400 | No |

### Example

#### JSON
```json
{
  "ike": {
    "preSharedKey": "321drowssaP"
  }
}
```

## Response

The response will be an entity representing the Site to Site VPN that was updated.

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
 "pendingTaskId": "54847",
 "accountAlias": "ACCT",
 "local": {
   "address": "4.3.2.1",
   "locationAlias": "WA1",
   "locationDescription": "WA1 - US West (Seattle)"               
   "subnets": [                          
     "10.10.10.0/24"
   ]
 },
 "remote": {
   "siteName": "Montreal Office",                
   "deviceType": "Cisco ASA5520 v8.3",        
   "address": "1.2.3.4",
   "subnets": [                          
     "10.1.1.0/24"
   ]
 },
 "ike": {
   "encryption": "aes128",               
   "hashing": "sha1_96",                 
   "diffieHelmanGroup": "group2",        
   "preSharedKey": "321drowssaP",
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
}
```
