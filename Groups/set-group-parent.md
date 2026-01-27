{{{
  "title": "Set Group Parent",
  "date": "02-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes the parent group of an existing group. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the parent of a given group.

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
| op | string| The operation to perform on a given property of the group. In this case, the value must be "set" for setting the parent group. |
| member | string | The property of the group to perform the operation on. In this case, the value will be "parentGroupId". |
| value | string | The value to set for the given member. This is the group identifier for the new parent group. |

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

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon making the changes successfully.
