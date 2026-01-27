{{{
  "title": "Get Cross Data Center Firewall Policy",
  "date": "5-23-2016",
  "author": "Anthony Hakim",
  "attachments": [],
  "contentIsHTML": false
}}}

Gets the details of a specific firewall policy associated with a given account, between networks in different data centers ("cross data center firewall policy"). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you need the details of a specific firewall policy between networks in different data centers.

  NOTE: This API operation is experimental only, and subject to change without notice. Please plan accordingly.

## URL

### Structure

    GET https://api.ctl.io/v2-experimental/crossDcFirewallPolicies/{sourceAccountAlias}/{dataCenter}/{policyId}

### Example

    GET https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/VA1/921670344d781378a8df6159c00bddea

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| sourceAccountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](https://www.ctl.io/api-docs/v2/#data-centers-get-data-center) API operation. | Yes |
| policyId | string | ID of the firewall policy  | Yes |

## Response

### Example

#### JSON
```json
{
    "id": "921670344d781378a8df6159c00bddea",
    "status": "active",
    "enabled": true,
    "sourceCidr": "10.2.2.0/24",
    "sourceAccount": "src",
    "sourceLocation": "va1",
    "destinationCidr": "10.1.1.0/24",
    "destinationAccount": "dest",
    "destinationLocation": "uc1",
    "links": [
        {
            "rel": "self",
            "href": "/v2-experimental/crossDcFirewallPolicies/src/va1/921670344d781378a8df6159c00bddea",
            "verbs": [
                "GET",
                "PUT",
                "DELETE"
            ]
        }
    ]
}
```
