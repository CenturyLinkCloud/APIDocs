{{{
  "title": "Execute Package",
  "date": "11-21-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Executes a single package on one or more servers. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](..Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to execute a Blueprint package that is available from within a given account on one or more servers. The list of available packages can be retrieved from the __Get Packages__ API operation.

## URL

### Structure

    POST https://api.ctl.io/v2/operations/{accountAlias}/servers/executePackage

### Example

    POST https://api.ctl.io/v2/operations/ALIAS/servers/executePackage

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
<h3>Content Properties</h3>
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
      <td>List of server IDs to run the package on.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>package</td>
      <td>complex</td>
      <td>The package entity describing which package to run on the specified servers.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Package Definition

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
      <td>packageId</td>
      <td>string</td>
      <td>Unique identifier of the package to execute.</td>
    </tr>
    <tr>
      <td>parameters</td>
      <td>complex</td>
      <td>Set of key-value pairs for setting the package-specific parameters defined.
        <br />
      </td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
        "servers": [
            "wa1aliaswb01"
        ],
        "package": {
            "packageId": "86567681-c79c-1234-a530-850708435c23",
            "parameters": {
                "AB.HelloWorld.Variable": "someValue"
            }
        }
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
      }
    ]
