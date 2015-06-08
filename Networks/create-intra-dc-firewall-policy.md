{{{
  "title": "Create an Intra Data Center Firewall Policy",
  "date": "6-12-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Creates a firewall policy for a given account in a given data center ("intra data center firewall policy"). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to create a firewall policy in a given data center for a given account.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly.

## URL

### Structure

    POST https://api.ctl.io/v2-experimental/firewallPolicies/{sourceAccountAlias}/{dataCenter}

### Example

    POST https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/WA1

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| sourceAccountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the target data center for the new policy. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| destinationAccount | string | Short code for a particular account | No |
| source | string | Source addresses for traffic on the originating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing), on the originating firewall | No |
| destination | string | Destination addresses for traffic on the terminating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | No |
| ports | string | Type of ports associated with the policy (i.e. FTP, HTTP, HTTPS, RDP, SSH/SFTP, etc.) and associated ranges if customized by the user | No |

### Examples

#### JSON
```json
{{
    "destinationAccount": "DEST_ALIAS",
    "source":["172.21.223.1/32", "172.21.223.2/32", "172.21.223.3/32"],
    "destination":["172.21.223.1/32", "172.21.223.2/32"],
    "ports":["tcp/1-600"]
}
```

## Response (need to verify)

The response will be an entity representing the new firewall policy that was created.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the firewall policy  |
| status | string | The state of the policy; either "active" (policy is available and working as expected), "error" (policy creation did not complete as expected) or "pending" (the policy is in the process of being created) |
| enabled | boolean | Indicates if the policy is enabled ("true") or disabled ("false") |
| source | string | Source addresses for traffic on the originating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) |
| destination | string | Destination addresses for traffic on the terminating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) |
| destinationAccount | string | Short code for a particular account |
| ports | string | Type of ports associated with the policy (i.e. FTP, HTTP, HTTPS, RDP, SSH/SFTP, etc.) and associated ranges if customized by the user |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this list of networks |

### Examples

#### JSON <JR still needs to scrub the id / source/destination data here>
```json
{
    "id": "de534c89464c4d648b350d994c0bc37c",
    "status": "active",
    "enabled": true,
    "source": [
        "172.21.223.1/32",
        "172.21.223.2/32",
        "172.21.223.3/32"
    ],
    "destination": [
        "172.21.223.1/32",
        "172.21.223.2/32"
    ],
    "destinationAccount": "DEST_ALIAS",
    "ports": [
        "any"
    ],
    "links": [
        {
            "rel": "self",
            "href": "http://api.ctlqa.io/v2-experimental/firewallPolicies/lyw/qa1/de534c89464c4d648b350d994c0bc37c",
            "verbs": [
                "GET",
                "PUT",
                "DELETE"
            ]
        }
    ]
}
```
