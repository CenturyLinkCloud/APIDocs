{{{
  "title": "Update Intra Data Center Firewall Policy",
  "date": "6-12-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Updates a given firewall policy associated with a given account in a given data center (an "intra data center firewall policy"). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to update a firewall policy in a given data center for a given account.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly.

## URL

### Structure

    PUT https://api.ctl.io/v2-experimental/firewallPolicies/{sourceAccountAlias}/{dataCenter}/{firewallPolicy}

### Example

    PUT https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/WA1/e46ef2500e1011e5b9390800200c9a66

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| sourceAccountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center associated with the policy of interest. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |
| destinationAccountAlias | string | Short code for a particular account | No |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| enabled | boolean | Indicates if the policy is enabled (`true`) or disabled (`false`) | No |
| source | string | Source addresses for traffic on the originating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | No |
| destination | string | Destination addresses for traffic on the terminating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | No |
| ports | string | Type of ports associated with the policy: `any` (all ports)`tcp/21` (for FTP), `tcp/990` (FTPS), `tcp/80` (HTTP 80), `tcp/8080` (HTTP 8080), `tcp/443` (HTTPS 443), `icmp` (PING), `tcp/3389` (RDP), and `tcp/22` (SSH/SFTP). Custom ports `udp/8000` and custom port ranges `tcp/1-600` are also supported. | No |


### Examples

#### JSON
```json
{
    "enabled":false,
    "source":["123.45.678.1/32"],
    "destination":["234.4.678.2/32"],
    "ports":["udp/8080"]
}
```

## Response

### Entity Definition

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon the successful update of firewall policy attributes.
