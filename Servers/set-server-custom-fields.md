{{{
  "title": "Set Server Custom Fields",
  "date": "02-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes the custom field values for an existing server. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the custom field values for a given server.

## URL

### Structure

    PATCH https://api.tier3.com/v2/servers/{accountAlias}/{serverId}

### Example

    PATCH https://api.tier3.com/v2/servers/ACCT/WA1ACCTSERV0101

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
      <td>The operation to perform on a given property of the server. In this case, the value must be "set" for setting the custom field values.
</td>
    </tr>
    <tr>
      <td>member</td>
      <td>string</td>
      <td>The property of the server to perform the operation on. In this case, the value will be "customFields".</td>
    </tr>
    <tr>
      <td>value</td>
      <td>array</td>
      <td>A list of id-value pairs for _all custom fields_ including all required values and other custom field values that you wish to set.<br/><br/>_Note: You must specify the complete list of custom field values to set on the server. If you want to change only one value, specify all existing field values along with the new value for the field you wish to change. To unset the value for an unrequired field, you may leave the field id-value pairing out, however all required fields must be included. (You can get existing custom field value info by using the <a href="/api-docs/v2#servers-get-server">Get Server</a> call to see all the details of the server or the <a href="/api-docs/v2#custom-fields-get-custom-fields">Get Custom Fields</a> call to see available custom fields for a given account.)_</td>
    </tr>
  </tbody>
</table>


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
