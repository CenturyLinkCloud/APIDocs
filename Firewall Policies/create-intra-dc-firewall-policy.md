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
| ports | string | Type of ports associated with the policy. Supported ports include: `any`, `icmp`, TCP and UDP with single ports (`tcp/123`, `udp/123`) and port ranges (`tcp/123-456`, `udp/123-456`). Some common ports include: `tcp/21` (for FTP), `tcp/990` (FTPS), `tcp/80` (HTTP 80), `tcp/8080` (HTTP 8080), `tcp/443` (HTTPS 443), `icmp` (PING), `tcp/3389` (RDP), and `tcp/22` (SSH/SFTP). | No |

### Examples

#### JSON
```json
{
    "destinationAccount": "DEST_ALIAS",
    "source":["123.45.223.1/32", "123.45.223.2/32", "123.45.223.3/32"],
    "destination":["123.45.223.1/32", "123.45.223.2/32"],
    "ports":["tcp/1-600"]
}
```

## Response

The response will be an entity representing the new firewall policy that was created.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this firewall policy |

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
