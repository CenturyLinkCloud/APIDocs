{{{
  "title": "Register Anywhere Server",
  "date": "11-07-2017",
  "author": "Anil Palepu",
  "attachments": [],
  "sticky": "false"
}}}

Registers a server as 'Anywhere Server' for Backup Anywhere service. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to register a server for Backup Anywhere Service.

## URL

### Structure

    POST https://api.backup.ctl.io/clc-backup-api/api/provisioning

### Example

    POST https://api.backup.ctl.io/clc-backup-api/api/provisioning
    
## Request

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| serverId | string | The name of the server being registered | Yes |
| osType | string | 'Linux' or 'Windows' -- OS of the server | Yes |

### Examples

#### JSON

    {
      "serverId": "My-AWS-Server-1",
      "osType": "Linux"
    }


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| provisioningToken | string | This is a provisioning token massaged into the installer package for one time use only |
| clcAccountAlias | string | The account alias to which the Anywhere Server is registered to |
| osType | string | 'Linux' or 'Windows' -- OS of the server |
| issuedTimestamp | long | This is the timestamp when Backup Anywhere installer package is used for a Anywhere server |
| redeemedTimestamp | long | This is the timestamp when SBS agent is installed on the Anywhere server and has communicated back to SBS Backup Anywhere infrastructure |
| revokedTimestamp | long | This is a timestamp which is set when SBS Backup Anywhere service is removed for a Anywhere Server |


### Examples

#### JSON

    {
      "provisioningToken": "PROVISIONbdb54aa4-a4fc-43a3-b452-3b4afda66096",
      "clcAccountAlias": "BAAS",
      "osType": "Linux",
      "issuedTimestamp": 1510090581000,
      "redeemedTimestamp": null,
      "revokedTimestamp": null
    }