{{{
  "title": "Set Maintenance Mode",
  "date": "11-21-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends a specified setting for maintenance mode per server to a list of servers and adds operation to queue. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to explicitly turn on or off maintenance mode on multiple servers. Specifically, this call can be used if you want set some servers to have maintenance mode on and others to have it off. If you want to set maintenance mode for servers to all on or all off, you can use the respective methods for [starting maintenance mode](start-maintenance-mode.md) or [stopping maintenance mode](stop-maintenance-mode.md) for multiple servers.

## URL

### Structure

    POST https://api.ctl.io/v2/operations/{accountAlias}/servers/setMaintenance

### Example

    POST https://api.ctl.io/v2/operations/ALIAS/servers/setMaintenance

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
      <td>servers</td>
      <td>array</td>
      <td>List of server ID and maintenance mode pairs to set.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Servers Definition

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
      <td>id</td>
      <td>string</td>
      <td>ID of server to set maintenance mode on or off</td>
    </tr>
    <tr>
      <td>inMaintenanceMode</td>
      <td>boolean</td>
      <td>Indicator of whether to place server in maintenance mode or not
        <br />
      </td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
      "servers":[
        {
          "id": "wa1aliaswb01",
          "inMaintenanceMode": "true"
        },
        {
          "id": "wa1aliaswb02",
          "inMaintenanceMode": "false"
        }
      ]
    }

## Response

The response will be an array containing one entity for each server that the operation was performed on.

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
      <td>server</td>
      <td>string</td>
      <td>ID of the server that the operation was performed on.</td>
    </tr>
    <tr>
      <td>isQueued</td>
      <td>boolean</td>
      <td>Boolean indicating whether the operation was successfully added to the queue.</td>
    </tr>
    <tr>
      <td>links</td>
      <td>complex</td>
      <td>Collection of entity links that point to resources related to this server operation.</td>
    </tr>
    <tr>
      <td>errorMessage</td>
      <td>string</td>
      <td>If something goes wrong or the request is not queued, this is the message that contains the details about what happened.</td>
    </tr>
  </tbody>
</table>

### Status Link Definition

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
      <td>The identifier of the job in queue. Can be passed to [Get Status](../Queue/get-status.md) call to retrieve status of job.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    [
      {
        "server":"wa1aliaswb01",
        "isQueued":true,
        "links":[
          {
            "rel":"status",
            "href":"/v2/operations/alias/status/wa1-12345",
            "id":"wa1-12345"
          }
        ]
      },
      {
        "server":"wa1aliaswb02",
        "isQueued":false,
        "errorMessage":"The operation cannot be queued because the server cannot be found or it is not in a valid state."
      }
    ]
