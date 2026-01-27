{{{
  "title": "Get All Regions",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "false"
}}}

Retrieves a list of backup storage regions which are available in Simple Backup Service. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to retrieve the list of backup storage regions which are available in Simple Backup Service.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/regions

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/regions


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| messages | Array[string] | A list of messages associated with the Storage Region |
| name | string | The name of the Storage Region |
| regionLabel | string | The label associated with the Storage Region |


### Examples

#### JSON

    [
      {
        "name": "APAC",
        "regionLabel": "APAC (Singapore)",
        "messages": null
      },
      {
        "name": "GERMANY",
        "regionLabel": "EU (Germany)",
        "messages": null
      },
      {
        "name": "GREAT BRITAIN",
        "regionLabel": "EU (Ireland)",
        "messages": null
      },
      {
        "name": "US EAST",
        "regionLabel": "US East",
        "messages": null
      },
      {
        "name": "US WEST",
        "regionLabel": "US West",
        "messages": null
      },
      {
        "name": "CANADA",
        "regionLabel": "Canada",
        "messages": [
          "Backups stored in this region are NOT encrypted at rest"
        ]
      }
    ]
