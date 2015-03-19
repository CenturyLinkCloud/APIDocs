{{{
  "title": "Get Public IP Address",
  "date": "11-23-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets the details for the public IP address of a server, including the specific set of protocols and ports allowed and any source IP restrictions. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to find out information about a specific public IP address for an existing server. This operation is linked to from the [Get Server](../Servers/get-server.md) response that lists all public IPs assigned to a server.

## URL

### Structure

    GET https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/publicIPAddresses/{publicIP}

### Example

    GET https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101/publicIPAddresses/12.34.56.789

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the server being queried. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |
| PublicIP | string | The specific public IP to return details about. A server may have more than one public IP, and the list of available ones can be retrieved from the call to [Get Server](../Servers/get-server.md). | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| internalIPAddress | string | The internal (private) IP address mapped to the public IP address. |
| ports | array | The set of accessible ports and protocols for the public IP address. |
| sourceRestrictions | array | The source IP address range allowed to access the new public IP address. Only traffic from this range will have access to the public IP on the specified ports. |

### Ports Definition

| Name | Type | Description |
| --- | --- | --- |
| protocol | string | The specific protocol to support for the given port(s). Should be either "tcp", "udp", or "icmp" (which is enabled by default). |
| port | integer | The port to open for the given protocol. If defining a range of ports, this represents the first port in the range. |
| portTo | integer | If defining a range of ports, optionally provide the last number of the range. |

### SourceRestrictions Definition

| Name | Type | Description |
| --- | --- | --- |
| cidr | string | The IP range allowed to access the public IP, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing). |

### Examples

#### JSON

    {
      "internalIPAddress":"10.11.12.13",
      "ports":[
        {
          "protocol":"ICMP",
          "port":0
        },
        {
          "protocol":"TCP",
          "port":80
        },
        {
          "protocol":"TCP",
          "port":443
        },
        {
          "protocol":"TCP",
          "port":8080,
          "portTo":8081
        },
        {
          "protocol":"UDP",
          "port":123
        }
      ],
      "sourceRestrictions":[
        {
          "cidr":"70.100.60.140/32"
        },
        {
          "cidr":"71.100.60.0/24"
        }
      ]
    }
