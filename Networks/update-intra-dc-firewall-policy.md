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

    PUT https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/WA1/de534c89464c4d648b350d994c0bc37c

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
| enabled | boolean | Indicates if the policy is enabled ("true") or disabled ("false") | No |
| source | string | Source addresses for traffic on the originating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | No |
| destination | string | Destination addresses for traffic on the terminating firewall, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) | No |
| ports | string | Type of ports associated with the policy (i.e. FTP, HTTP, HTTPS, RDP, SSH/SFTP, etc.) and associated ranges if customized by the user | No |


### Examples

#### JSON
```json
{
    "enabled":false,
    "source":["172.21.223.1/32"],
    "destination":["172.21.223.2/32"],
    "ports":["udp/8080"]
}
```

## Response (need to verify)

### Entity Definition

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon the successful update of firewall policy attributes.
