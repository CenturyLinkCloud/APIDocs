{{{
  "title": "Update Public IP Address",
  "date": "11-23-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Updates a public IP address on an existing server, allowing access to it on a given set of protocols and ports as well as restricting access based on a source IP range. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to update the ports and protocols or source IP restrictions for a public IP address on an existing server.

## URL

### Structure

    PUT https://api.tier3.com/v2/servers/{accountAlias}/{serverId}/publicIPAddresses/{publicIP}

### Example

    PUT https://api.tier3.com/v2/servers/ACCT/WA1ACCTSERV0101/publicIPAddresses/12.34.56.789

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
      <td>ID of the server with the public IP to update. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PublicIP</td>
      <td>string</td>
      <td>The specific public IP to update. A server may have more than one public IP, and the list of available ones can be retrieved from the call to <a href="/api-docs/v2#servers-get-server">Get Server</a>.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

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
      <td>int</td>
      <td>The port to open for the given protocol. If defining a range of ports, this represents the first port in the range.</td>
    </tr>
    <tr>
      <td>portTo</td>
      <td>int</td>
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

The response is a link to the <a href="/api-docs/v2#queue-get-status">Get Status</a> operation so the asynchronous job can be tracked. Once successfully completed, the public IP address will be available for use as specified.

### Entity Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>

    <tr>
      <td>rel</td>
      <td>string</td>
      <td>status</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/operations/[ALIAS]/status/[ID]</td>
      <td>Address of the server creation job in the queue</td>
    </tr>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>[ID]</td>
      <td>The identifier of the job in queue. Can be passed to&nbsp;<a href="/api-docs/v2#queue-get-status">Get Status</a>&nbsp;call to retrieve status of job.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
      "rel":"status",
      "href":"/v2/operations/alias/status/wa1-12345",
      "id":"wa1-12345"
    }
