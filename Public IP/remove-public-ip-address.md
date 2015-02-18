{{{
  "title": "Remove Public IP Address",
  "date": "11-23-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Releases the given public IP address of a server so that it is no longer associated with the server and available to be claimed again by another server. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to stop using a specific public IP address on an existing server.

## URL

### Structure

    DELETE https://api.tier3.com/v2/servers/{accountAlias}/{serverId}/publicIPAddresses/{publicIP}

### Example

    DELETE https://api.tier3.com/v2/servers/ACCT/WA1ACCTSERV0101/publicIPAddresses/12.34.56.789

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
      <td>ID of the server with the public IP address to remove. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PublicIP</td>
      <td>string</td>
      <td>The specific public IP to remove. A server may have more than one public IP, and the list of available ones can be retrieved from the call to <a href="/api-docs/v2#servers-get-server">Get Server</a>.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

## Response

The response is a link to the <a href="/api-docs/v2#queue-get-status">Get Status</a> operation so the asynchronous job can be tracked. Once successfully completed, the public IP address will no longer be associated with the server.

### Entity Definition

<table>
  <thead>
    <th>Name
    </th>
    <th>Type
    </th>
    <th>Value
    </th>
    <th>Description
    </th>
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
      <td>The identifier of the job in queue. Can be passed to <a href="/api-docs/v2#queue-get-status">Get Status</a> call to retrieve status of job.</td>
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
