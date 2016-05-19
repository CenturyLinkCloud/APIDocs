{{{
  "title": "Get Cross Data Center Firewall Policy",
  "date": "5-24-2016",
  "author": "Anthony Hakim",
  "attachments": []
}}}

Gets the details of a specific firewall policy associated with a given account between networks in different data centers (an "cross data center firewall policy"). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need the details of a specific firewall policy in a given data center for a given account.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly.

## URL

### Structure

    GET https://api.ctl.io/v2-experimental/firewallPolicies/{sourceAccountAlias}/{dataCenter}/{firewallPolicy}

### Example

    GET https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/WA1/1ac853b00e1011e5b9390800200c9a66

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| sourceAccountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |
| firewallPolicy | string | ID of the firewall policy  | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the firewall policy  |
| status | string | The state of the policy; either `active` (policy is available and working as expected), `error` (policy creation did not complete as expected) or `pending` (the policy is in the process of being created) |
| enabled | boolean | Indicates if the policy is enabled (`true`) or disabled (`false`) |
| source | string | Source addresses for traffic on the originating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) |
| destination | string | Destination addresses for traffic on the terminating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) |
| destinationAccount | string | Short code for a particular account |
| ports | string | Type of ports associated with the policy. Supported ports include: `any`, `icmp`, TCP and UDP with single ports (`tcp/123`, `udp/123`) and port ranges (`tcp/123-456`, `udp/123-456`). Some common ports include: `tcp/21` (for FTP), `tcp/990` (FTPS), `tcp/80` (HTTP 80), `tcp/8080` (HTTP 8080), `tcp/443` (HTTPS 443), `icmp` (PING), `tcp/3389` (RDP), and `tcp/22` (SSH/SFTP). |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this list of firewall policies |

### Examples

#### JSON
```json
{
    "id": "1ac853b00e1011e5b9390800200c9a6",
    "status": "active",
    "enabled": true,
    "source": [
        "123.45.678.1/32",
        "123.45.678.2/32",
        "123.45.678.3/32"
    ],
    "destination": [
        "245.21.223.1/32",
        "245.21.223.2/32"
    ],
    "destinationAccount": "DEST_ALIAS",
    "ports": [
        "any"
    ],
    "links": [
        {
            "rel": "self",
            "href": "https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/WA1/1ac853b00e1011e5b9390800200c9a6",
            "verbs": [
                "GET",
                "PUT",
                "DELETE"
            ]
        }
    ]
}
```
