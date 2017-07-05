{{{
  "title": "Get Intra Data Center Firewall Policy List",
  "date": "6-12-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Gets the list of firewall policies associated with a given account in a given data center ("intra data center firewall policies"). Users can optionally filter results by requesting policies associated with a second "destination" account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need the list of available firewall policies in a given data center for a given account. Using that list of firewall policies, you can then query for a [specific policy](get-intra-dc-firewall-policy.md) in a given data center.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly.

## URL

### Structure

    GET https://api.ctl.io/v2-experimental/firewallPolicies/{sourceAccountAlias}/{dataCenter}?destinationAccount={destinationAccountAlias}

### Example

    GET https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/WA1?destinationAccount=DEST_ALIAS

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| sourceAccountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |
| destinationAccountAlias | string | Short code for a particular account | No |


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the firewall policy  |
| status | string | The state of the policy: either `active` (policy is available and working as expected), `error` (policy creation did not complete as expected) or `pending` (the policy is in the process of being created) |
| enabled | boolean | Indicates if the policy is enabled (`true`) or disabled (`false`) |
| source | string | Source addresses for traffic on the originating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) |
| destination | string | Destination addresses for traffic on the terminating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) |
| destinationAccount | string | Short code for a particular account |
| ports | string | Type of ports associated with the policy. Supported ports include: `any`, `icmp`, TCP and UDP with single ports (`tcp/123`, `udp/123`) and port ranges (`tcp/123-456`, `udp/123-456`). Some common ports include: `tcp/21` (for FTP), `tcp/990` (FTPS), `tcp/80` (HTTP 80), `tcp/8080` (HTTP 8080), `tcp/443` (HTTPS 443), `icmp` (PING), `tcp/3389` (RDP), and `tcp/22` (SSH/SFTP). |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this list of firewall policies |

### Examples

#### JSON
```json
[
    {
        "id": "c59b96600e0d11e5b9390800200c9a66",
        "status": "active",
        "enabled": true,
        "source": [
            "123.45.678.1/32",
            "123.45.678.2/32",
            "123.45.678.3/32"
        ],
        "destination": [
            "234.56.789.1/32",
            "234.56.789.2/32"
        ],
        "destinationAccount": "DEST_ALIAS",
        "ports": [
            "any"
        ],
        "links": [
            {
                "rel": "self",
                "href": "https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/WA1/c59b96600e0d11e5b9390800200c9a66",
                "verbs": [
                    "GET",
                    "PUT",
                    "DELETE"
                ]
            }
        ]
    },
    {
        "id": "bbb377290e0e11e5b9390800200c9a66",
        "status": "active",
        "enabled": false,
        "source": [
            "145.67.890.1/32",
            "145.67.890.2/32",
            "145.67.890.3/32"
        ],
        "destination": [
            "156.78.901.1/32",
            "156.78.901.2/32"
        ],
        "destinationAccount": "DEST_ALIAS",
        "ports": [
            "any"
        ],
        "links": [
            {
                "rel": "self",
                "href": "https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/WA1/bbb377290e0e11e5b9390800200c9a66",
                "verbs": [
                    "GET",
                    "PUT",
                    "DELETE"
                ]
            }
        ]
    },
    {
        "id": "d56587800e0e11e5b9390800200c9a66",
        "status": "active",
        "enabled": true,
        "source": [
            "123.45.678.1/32"
        ],
        "destination": [
            "234.23.435.200/32"
        ],
        "destinationAccount": "DEST_ALIAS",
        "ports": [
            "tcp/8080",
            "tcp/1-8000"
        ],
        "links": [
            {
                "rel": "self",
                "href": "https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/WA1/d56587800e0e11e5b9390800200c9a66",
                "verbs": [
                    "GET",
                    "PUT",
                    "DELETE"
                ]
            }
        ]
    },
]
```
