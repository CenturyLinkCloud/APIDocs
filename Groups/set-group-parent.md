{{{
  "title": "Set Group Name/Description",
  "date": "02-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes the name and description of an existing group. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](..Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the name or description of a given group.

## URL

### Structure

    PATCH https://api.ctl.io/v2/groups/{accountAlias}/{groupId}

### Example

    PATCH https://api.ctl.io/v2/groups/ACCT/2a5c0b9662cf4fc8bf6180f139facdc0

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
      <td>GroupId</td>
      <td>string</td>
      <td>ID of the group to update. Retrieved from query to containing group, or by looking at the URL when viewing a group in the Control Portal.</td>
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
      <td>A list of properties, values, and the operations to perform with them for the group.</td>
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
      <td>The operation to perform on a given property of the group. In this case, the value must be "set" for setting the parent group.
</td>
    </tr>
    <tr>
      <td>member</td>
      <td>string</td>
      <td>The property of the group to perform the operation on. In this case, the value will be "parentGroupId".</td>
    </tr>
    <tr>
      <td>value</td>
      <td>string</td>
      <td>The value to set for the given member. This is the group identifier for the new parent group.</td>
    </tr>
  </tbody>
</table>


### Examples

#### JSON

    [
       {
          "op":"set",
          "member":"parentGroupId",
          "value":"af7552c50e1b40b28d8023ed5eeaa74c"
       }
    ]

## Response

The response will not contain JSON content, but should return a standard HTTP `200 OK` response upon making the changes successfully.
