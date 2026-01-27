{{{
  "title": "Set Group Name/Description",
  "date": "02-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes the name and description of an existing group. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the name or description of a given group.

## URL

### Structure

    PATCH https://api.ctl.io/v2/groups/{accountAlias}/{groupId}

### Example

    PATCH https://api.ctl.io/v2/groups/ACCT/2a5c0b9662cf4fc8bf6180f139facdc0

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| GroupId | string | ID of the group to update. Retrieved from query to containing group, or by looking at the URL when viewing a group in the Control Portal. | Yes |


### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| patchOperation | array | A list of properties, values, and the operations to perform with them for the group. | Yes |

### PatchOperation Definition

| Name | Type | Description |
| --- | --- | --- |
| op | string | The operation to perform on a given property of the group. In this case, the value must be "set" for setting the name and description. |
| member | string | The property of the group to perform the operation on. In this case, the value will be either "name" or "description". |
| value | string | The value to set for the given member. This is the name or description to set for the group. |


### Examples

#### JSON

    [
       {
          "op":"set",
          "member":"name",
          "value":"New Name"
       },
       {
          "op":"set",
          "member":"description",
          "value":"New Description"
       }
    ]

## Response

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon making the changes successfully.
