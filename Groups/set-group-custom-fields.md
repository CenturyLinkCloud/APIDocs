{{{
  "title": "Set Group Custom Fields",
  "date": "02-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes the custom field values for an existing group. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the custom field values for a given group.

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

|Name|Type|Description|
|---|---|---|
|op|string|The operation to perform on a given property of the group. In this case, the value must be "set" for setting the custom field values.|
|member|string|The property of the group to perform the operation on. In this case, the value will be "customFields".|
|value|array|A list of id-value pairs for _all custom fields_ including all required values and other custom field values that you wish to set.<br/><br/>_Note: You must specify the complete list of custom field values to set on the group. If you want to change only one value, specify all existing field values along with the new value for the field you wish to change. To unset the value for an unrequired field, you may leave the field id-value pairing out, however all required fields must be included. (You can get existing custom field value info by using the [Get Group](get-group.md) call to see all the details of the group or the [Get Custom Fields](../Custom Fields/get-custom-fields.md) call to see available custom fields for a given account.)_|


### Examples

#### JSON

    [
       {
          "op":"set",
          "member":"customFields",
          "value":[
             {
                "id":"dba67b154f774a1fb413ddfa3dc4ac1d",
                "value":"Required Value 1"
             },
             {
                "id":"58f83bf6675846769ee6cb091ce3561e",
                "value":"Optional Value 1"
             },
             {
                "id":"22f002e08f3b46d9a8b38ecd4c6df7f9",
                "value":"Required Value 2"
             }
          ]
       }
    ]

## Response

The response will not contain JSON content, but should return a standard HTTP `200 OK` response upon making the changes successfully.
