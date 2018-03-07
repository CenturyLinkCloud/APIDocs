{{{
  "title": "Get Anywhere Server List",
  "date": "03-07-2018",
  "author": "Kyle Miller",
  "attachments": [],
  "sticky": "false"
}}}

Get a list of SBS Anywhere servers. The id field can be used as serverIds to create server policies for an Anywhere server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get a list of SBS Anywhere servers.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/datacenters/anywhereServers

### Example

	GET https://api.backup.ctl.io/clc-backup-api/api/datacenters/anywhereServers

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| anywhereServerAliases | Array[Anywhere Server] | Array of AnywhereServers corresponding to the user's CLC alias |


### Examples

#### JSON

    {
      [2]
      0:  {
              "id":"026b28ae-9b1f-4a3b-a3ab-89da0ebb68af",
			  "accountAlias":"ACME",
			  "osType":"Linux",
			  "serverAlias":"my-linux-server"
	      }
      1:  {
              "id":"a3dc3866-68b7-4482-b645-66163ffbe4a2",
			  "accountAlias":"ACME",
			  "osType":"Windows",
			  "serverAlias":"My.Windows.Server"
	      }
    }
