{{{
  "title": "Get Public IP Address",
  "date": "11-23-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets the details for the public IP address of a server, including the specific set of protocols and ports allowed and any source IP restrictions. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to find out information about a specific public IP address for an existing server. This operation is linked to from the <a href="/api-docs/v2#servers-get-server">Get Servers</a> response that lists all public IPs assigned to a server.

## URL

### Structure

    GET https://api.tier3.com/v2/servers/{accountAlias}/{serverId}/publicIPAddresses/{publicIP}

### Example

    GET https://api.tier3.com/v2/servers/ACCT/WA1ACCTSERV0101/publicIPAddresses/12.34.56.789

## Request

### URI Parameters

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
      <td>AccountAlias</td>
      <td>string</td>
      <td>Short code for a particular account</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ServerId</td>
      <td>string</td>
      <td>ID of the server being queried. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PublicIP</td>
      <td>string</td>
      <td>The specific public IP to return details about. A server may have more than one public IP, and the list of available ones can be retrieved from the call to <a href="/api-docs/v2#servers-get-server">Get Server</a>.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

## Response

### Entity Definition

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
      <td>internalIPAddress</td>
      <td>string</td>
      <td>The internal (private) IP address mapped to the public IP address.</td>
    </tr>
    <tr>
      <td>ports</td>
      <td>array</td>
      <td>The set of accessible ports and protocols for the public IP address.</td>
    </tr>
    <tr>
      <td>sourceRestrictions</td>
      <td>array</td>
      <td>The source IP address range allowed to access the new public IP address. Only traffic from this range will have access to the public IP on the specified ports.</td>
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
      <td>The specific protocol to support for the given port(s). Should be either "tcp", "udp", or "icmp" (which is enabled by default).</td>
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
