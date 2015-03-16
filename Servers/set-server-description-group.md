{{{
  "title": "Set Server Description/Group",
  "date": "02-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes the description and parent group of an existing server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](..Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the description or the parent group of a given server.

## URL

### Structure

    PATCH https://api.ctl.io/v2/servers/{accountAlias}/{serverId}

### Example

    PATCH https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101

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
      <td>ID of the server to update. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal.</td>
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
      <td>patchOperation</td>
      <td>array</td>
      <td>A list of properties, values, and the operations to perform with them for the server.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### PatchOperation Definition

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
      <td>op</td>
      <td>string</td>
      <td>The operation to perform on a given property of the server. In this case, the value must be "set" for setting the description and parent group.
</td>
    </tr>
    <tr>
      <td>member</td>
      <td>string</td>
      <td>The property of the server to perform the operation on. In this case, the value will be either "description" or "groupId".</td>
    </tr>
    <tr>
      <td>value</td>
      <td>string</td>
      <td>The value to set for the given member. This is either the description of the server to set, or the unique identifier of the group to set as the parent.</td>
    </tr>
  </tbody>
</table>


### Examples

#### JSON

    [
       {
          "op":"set",
          "member":"description",
          "value":"New Description"
       },
       {
          "op":"set",
          "member":"groupId",
          "value":"wa1-1002"
       }
    ]

## Response

The response will not contain JSON content, but should return a standard HTTP `200 OK` response upon making the changes successfully.
