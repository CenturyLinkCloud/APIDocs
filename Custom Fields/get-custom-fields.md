{{{
  "title": "Get Custom Fields",
  "date": "02-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Retrieves the custom fields defined for a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation to find out the details of what custom fields are defined for an account.

## URL

### Structure

    GET https://api.ctl.io/v2/accounts/{accountAlias}/customFields

### Example

    GET https://api.ctl.io/v2/accounts/ACCT/customFields

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

## Response

The response will be an array containing one entity for each custom field defined in the given account.

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
      <td>id</td>
      <td>string</td>
      <td>Unique identifier of the custom field.</td>
    </tr>
    <tr>
      <td>name</td>
      <td>string</td>
      <td>Friendly name of the custom field as it appears in the UI.</td>
    </tr>
    <tr>
      <td>isRequired</td>
      <td>boolean</td>
      <td>Boolean value representing whether or not a value is required for this custom field.</td>
    </tr>
    <tr>
      <td>type</td>
      <td>string</td>
      <td>The type of custom field defined. Will be either "text" (free-form text field), "checkbox" (boolean value), or "option" (dropdown list).</td>
    </tr>
    <tr>
      <td>options</td>
      <td>array</td>
      <td>Array of name-value pairs corresponding to the options defined for this field. (Empty for "text" or "checkbox" field types.)</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    [
      {
        "id":"dba67b156f77123fb413ddfa3dc4ac1d",
        "name":"Cost Center",
        "isRequired":false,
        "type":"text",
        "options":[]
      },
      {
        "id":"58f83af6123846769ee6cb091ce3561e",
        "name":"Production",
        "isRequired":true,
        "type":"checkbox",
        "options":[]
      },
      {
        "id":"22f002123e3b46d9a8b38ecd4c6df7f9",
        "name":"Color",
        "isRequired":true,
        "type":"option",
        "options":[
          {
            "name":"red",
            "value":"Red"
          },
          {
            "name":"blue",
            "value":"Blue"
          }
        ]
      }
    ]
