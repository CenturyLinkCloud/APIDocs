{{{
  "title": "Add Public IP Address",
  "date": "11-23-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Claims a public IP address and associates it with a server, allowing access to it on a given set of protocols and ports. It may also be set to restrict access based on a source IP range. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to add a public IP address to an existing server. The public IP can be exposed on multiple protocols and ports and also be set to restrict access based on source IP ranges.

## URL

### Structure

    POST https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/publicIPAddresses

### Example

    POST https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101/publicIPAddresses

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the server being queried. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| internalIPAddress | string | The internal (private) IP address to map to the new public IP address. If not provided, one will be assigned for you. | No |
| ports | array | The set of ports and protocols to allow access to for the new public IP address. Only these specified ports on the respective protocols will be accessible when accessing the server using the public IP address claimed here. | Yes |
| sourceRestrictions | array | The source IP address range allowed to access the new public IP address. Used to restrict access to only the specified range of source IPs. | No |

### Ports Definition

| Name | Type | Description |
| --- | --- | --- |
| protocol | string | The specific protocol to support for the given port(s). Should be one of the following: "tcp", "udp", or "icmp". |
| port | integer | The port to open for the given protocol. If defining a range of ports, this represents the first port in the range. |
| portTo | integer | If defining a range of ports, optionally provide the last number of the range. |

### SourceRestrictions Definition

| Name | Type | Description |
| --- | --- | --- |
| cidr | string | The IP range allowed to access the public IP, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing). |

### Examples

#### JSON

    {
      "ports":[
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

## Response

The response is a link to the [Get Status](../Queue/get-status.md) operation so the asynchronous job can be tracked. Once successfully completed, the public IP address will be available for use as specified.

### Entity Definition

| Name | Type | Value | Description |
| --- | --- | --- | --- |
| rel | string | status | The link type |
| href | string | /v2/operations/[ALIAS]/status/[ID] | Address of the job in the queue |
| id | string | [ID] | The identifier of the job in queue. Can be passed to [Get Status](../Queue/get-status.md) call to retrieve status of job. |

### Examples

#### JSON

    {
      "rel":"status",
      "href":"/v2/operations/alias/status/wa1-12345",
      "id":"wa1-12345"
    }
