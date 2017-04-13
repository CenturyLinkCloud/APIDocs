{{{
  "title": "Get OS Types",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "false"
}}}

Returns the list of valid OS types supported by Simple Backup Service. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to retrieve the list of supported OS types.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/osTypes

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/osTypes


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| osTypes | Array[string] | Array of string values corresponding to each supported OS type |


### Examples

#### JSON

    [
      "Linux",
      "Windows]
    ]
