{{{
  "title": "Create a Cross Data Center Firewall Policy",
  "date": "5-24-2016",
  "author": "Anthony Hakim",
  "attachments": [],
  "contentIsHTML": false
}}}

Creates a firewall policy for a given account between networks in different data centers ("cross data center firewall policy"). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you need to create a firewall policy between networks in different data centers for a given account.

  NOTE: This API operation is experimental only, and subject to change without notice. Please plan accordingly.

## URL

### Structure

    POST https://api.ctl.io/v2-experimental/crossDcFirewallPolicies/{accountId}/{locationId}

### Example

    POST https://api.ctl.io/v2-experimental/crossDcFirewallPolicies/SRC_ALIAS/WA1

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountId | string | Short code for a particular account | Yes |
| locationId | string | Short string representing the target data center for the new policy. Valid codes can be retrieved from the [Get Data Center List](https://www.ctl.io/api-docs/v2/#data-centers-get-data-center) API operation. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| destinationAccountId | string | Short code for a particular account | Yes |
| destinationLocationId | string | Short code for a particular location | Yes |
| destinationCidr | string | Destination address for traffic on the terminating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | Yes |
| enabled | string | Indicates if the policy is enabled (`true`) or disabled (`false`) | Yes |
| sourceCidr | string | Source address for traffic on the originating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing), on the originating firewall | Yes |

### Example

#### JSON
```json
{
    "destinationAccountId" : "accountAlias",
    "destinationLocationId" : "UC1",
    "destinationCidr" : "10.124.15.0/24"
    "enabled" : true,
    "sourceCidr" : "10.81.10.0/24"
}
```

## Response

The response will be an entity representing the new firewall policy that was created.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| links | array | Collection of [entity links](https://www.ctl.io/api-docs/v2/#getting-started-api-v20-links-framework) that point to resources related to this firewall policy |

### Examples

#### JSON
```json
{
    "links": [
        {
            "rel": "self",
            "href": "https://api.ctl.io/v2-experimental/firewallPolicies/DEST_ALIAS/WA1/71f912d00e1c11e5b9390800200c9a66",
            "verbs": [
                "GET",
                "PUT",
                "DELETE"
            ]
        }
    ]
}
```
