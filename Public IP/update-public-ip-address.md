{{{
  "title": "Update Public IP Address",
  "date": "11-23-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Updates a public IP address on an existing server, allowing access to it on a given set of protocols and ports as well as restricting access based on a source IP range. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to update the ports and protocols or source IP restrictions for a public IP address on an existing server.

## URL

### Structure

    PUT https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/publicIPAddresses/{publicIP}

### Example

    PUT https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101/publicIPAddresses/12.34.56.789

## Request

### URI Parameters

|Name|Type|Description|Req.|
|---|---|---|---|
|AccountAlias|string|Short code for a particular account|Yes|
|ServerId|string|ID of the server being queried. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal.|Yes|
|PublicIP|string|The specific public IP to return details about. A server may have more than one public IP, and the list of available ones can be retrieved from the call to [Get Server](../Servers/get-server.md).|Yes|

### Content Properties

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Req.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ports</td>
      <td>array</td>
      <td>The set of ports and protocols to allow access to for the public IP address. Only these specified ports on the respective protocols will be accessible when accessing the server using the public IP address specified here.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>sourceRestrictions</td>
      <td>array</td>
      <td>The source IP address range allowed to access the public IP address. Used to restrict access to only the specified range of source IPs.</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

### Ports Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>protocol</td>
      <td>string</td>
      <td>The specific protocol to support for the given port(s). Should be one of the following: "tcp", "udp", or "icmp".</td>
    </tr>
    <tr>
      <td>port</td>
      <td>integer</td>
      <td>The port to open for the given protocol. If defining a range of ports, this represents the first port in the range.</td>
    </tr>
    <tr>
      <td>portTo</td>
      <td>integer</td>
      <td>If defining a range of ports, optionally provide the last number of the range.</td>
    </tr>
  </tbody>
</table>

### SourceRestrictions Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>cidr</td>
      <td>string</td>
      <td>The IP range allowed to access the public IP, specified using <a href="http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing" target="_blank">CIDR notation</a>.</td>
    </tr>
  </tbody>
</table>

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

|Name|Type|Value|Description|
|---|---|---|---|
|rel|string|status|The link type|
|href|string|/v2/operations/[ALIAS]/status/[ID]|Address of the job in the queue|
|id|string|[ID]|The identifier of the job in queue. Can be passed to [Get Status](../Queue/get-status.md) call to retrieve status of job.|

### Examples

#### JSON

    {
      "rel":"status",
      "href":"/v2/operations/alias/status/wa1-12345",
      "id":"wa1-12345"
    }
