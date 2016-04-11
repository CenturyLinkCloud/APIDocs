{{{
  "title": "Get Servers By Datacenter",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "true"
}}}

Get a list of servers based on CLC Data Center. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get a list of servers associated with a CLC Data Center.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api//api/datacenters/{datacenter}/servers

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/datacenters/VA1%20-%20US%20East%20(Sterling)/servers

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| datacenter | string | CLC Data Center | Yes |


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| list | Array[string] | Array of string values corresponding to each server |


### Examples

#### JSON

    {
      [3]
      0:  "VA1BAAPXAMPLE01"
      1:  "VA1BAAPXAMPLE02"
      2:  "VA1BAAPXAMPLE03"
    }
