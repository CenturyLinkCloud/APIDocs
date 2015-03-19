{{{
  "title": "Get Custom Fields",
  "date": "02-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Retrieves the custom fields defined for a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to find out the details of what custom fields are defined for an account.

## URL

### Structure

    GET https://api.ctl.io/v2/accounts/{accountAlias}/customFields

### Example

    GET https://api.ctl.io/v2/accounts/ACCT/customFields

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

## Response

The response will be an array containing one entity for each custom field defined in the given account.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | Unique identifier of the custom field. |
| name | string | Friendly name of the custom field as it appears in the UI. |
| isRequired | boolean | Boolean value representing whether or not a value is required for this custom field. |
| type | string | The type of custom field defined. Will be either "text" (free-form text field), "checkbox" (boolean value), or "option" (dropdown list). |
| options | array | Array of name-value pairs corresponding to the options defined for this field. (Empty for "text" or "checkbox" field types.) |

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
