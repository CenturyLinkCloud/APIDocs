{{{
  "title": "Get Datacenter List",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "false"
}}}

DESCRIPTION. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to . It can be used to .

## URL

### Structure

    GET https://api-va1.backup.ctl.io/clc-backup-api/api/datacenters

### Example

    GET https://api-va1.backup.ctl.io/clc-backup-api/api/datacenters


## Response

### List Definition

| Name | Type | Description |
| --- | --- | --- |
| list | Array[string] | Array of string values corresponding to each datacenter |


### Examples

#### JSON

    {

    }
