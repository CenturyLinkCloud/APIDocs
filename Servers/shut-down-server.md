{{{
  "title": "Shut Down Server",
  "date": "11-19-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends the shut down operation to a list of servers and adds operation to queue. (See <a href="/knowledge-base/servers/descriptions-of-servergroup-power-commands/">Description of Server Group Power Commands</a> for details on how the shut down operation is used.) Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to shut down a single server or group of servers. It should be used in conjunction with the <a href="/api-docs/v2#queue-get-status">Get Status</a> operation to check the result of the shut down command.

### Supported HTTP Verbs

Requests to this endpoint are done via HTTP POST.

## URL

### Structure

    https://api.tier3.com/v2/operations/{accountAlias}/servers/shutDown

### Example

    https://api.tier3.com/v2/operations/ALIAS/servers/shutDown

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
      <td>serverIds</td>
      <td>array</td>
      <td>List of server IDs to perform shut down operation on.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    [

       "WA1ALIASWB01",

       "WA1ALIASWB02"

    ]

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

### Links Definition

<table style="border: 1px solid gray; border-image: none; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="100"><strong>Name</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="75"><strong>Type</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="250"><strong>Value</strong></td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;" rowspan="3">Status Link</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">rel</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">string</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">status</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">The link type</td>
</tr>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">href</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">string</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">/v2/operations/[ALIAS]/status/[ID]</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">Address of the resource itself</td>
</tr>
<tr>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">id</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">string</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">[ID]</td>
<td style="padding: 5px; border: 1px solid gray; border-image: none;">The identifier of the job in queue. Can be passed to <a href="/api-docs/v2#queue-get-status">Get Status</a> call to retrieve status of job.</td>
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