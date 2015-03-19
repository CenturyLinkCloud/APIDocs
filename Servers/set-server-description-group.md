{{{
  "title": "Set Server Description/Group",
  "date": "02-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes the description and parent group of an existing server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the description or the parent group of a given server.

## URL

### Structure

    PATCH https://api.ctl.io/v2/servers/{accountAlias}/{serverId}

### Example

    PATCH https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the server to update. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |


### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| patchOperation | array | A list of properties, values, and the operations to perform with them for the server. | Yes |

### PatchOperation Definition

| Name | Type | Description |
| --- | --- | --- |
| op | string | The operation to perform on a given property of the server. In this case, the value must be "set" for setting the description and parent group. |
| member | string | The property of the server to perform the operation on. In this case, the value will be either "description" or "groupId". |
| value | string | The value to set for the given member. This is either the description of the server to set, or the unique identifier of the group to set as the parent. |


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
          "value":"2a5c0b9662cf4fc8bf6180f139facdc0"
       }
    ]

## Response

The response will not contain JSON content, but should return a standard HTTP `200 OK` response upon making the changes successfully.
