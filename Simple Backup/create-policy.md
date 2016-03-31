{{{
  "title": "Create Policy",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "true"
}}}

DESCRIPTION. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to . It can be used to .

## URL

### Structure

    GET https://api-va1.backup.ctl.io/clc-backup-api/

### Example

    GET https://api-va1.backup.ctl.io/clc-backup-api/

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |


## Response

### Server Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the server being queried |


### Details Definition

| Name | Type | Description |
| --- | --- | --- |
| ipAddresses | complex | Details about IP addresses associated with the server |


### Examples

#### JSON

    {

    }
