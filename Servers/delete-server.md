{{{
  "title": "Delete Server",
  "date": "11-24-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends the delete operation to a given server and adds operation to queue. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete a server that is no longer being used.

### Supported HTTP Verbs

Requests to this endpoint are done via HTTP DELETE.

## URL

### Structure

    https://api.tier3.com/v2/servers/{accountAlias}/{serverId}

### Example

    https://api.tier3.com/v2/servers/ACCT/WA1ACCTWB01

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
      <td>ID of the server to be deleted. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal.</td>
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
      <td>server</td>
      <td>string</td>
      <td>ID of the server that is being deleted.</td>
    </tr>
    <tr>
      <td>isQueued</td>
      <td>boolean</td>
      <td>Boolean indicating whether the delete operation was successfully added to the queue.</td>
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

    {
      "server":"wa1acctwb01",
      "isQueued":true,
      "links":[
        {
          "rel":"status",
          "href":"/v2/operations/alias/status/wa1-12345",
          "id":"wa1-12345"
        }
      ]
    }