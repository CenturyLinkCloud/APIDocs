{{{
  "title": "Get Datacenter List",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "false"
}}}

Get a list of CLC Data Centers. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get a list of CLC Data Centers.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/datacenters

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/datacenters


## Response

### List Definition

| Name | Type | Description |
| --- | --- | --- |
| list | Array[string] | Array of string values corresponding to each datacenter |


### Examples

#### JSON

    {
      [13]
      0:  "CA1 - Canada (Vancouver)"
      1:  "CA2 - Canada (Toronto)"
      2:  "CA3 - Canada (Toronto)"
      3:  "DE1 - Germany (Frankfurt)"
      4:  "GB1 - Great Britain (Portsmouth)"
      5:  "GB3 - Great Britain (Slough)"
      6:  "IL1 - US Central (Chicago)"
      7:  "NY1 - US East (New York)"
      8:  "SG1 - APAC (Singapore)"
      9:  "UC1 - US West (Santa Clara)"
      10:  "UT1 - US Central (Salt Lake City)"
      11:  "VA1 - US East (Sterling)"
      12:  "WA1 - US West (Seattle)"
    }
