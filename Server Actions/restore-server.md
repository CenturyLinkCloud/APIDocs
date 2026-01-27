{{{
  "title": "Restore Server",
  "date": "02-27-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Restores a given archived server to a specified group. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to restore a server that has been archived.

## URL

### Structure

    POST https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/restore

### Example

    POST https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101/restore

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the archived server to restore. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| targetGroupId | string | The unique identifier of the target group to restore the server to. | Yes |


### Examples

#### JSON

    {
      "targetGroupId": "2a5c0b9662cf4fc8bf6180f139facdc0"
    }

## Response

The response is a link to the [Get Status](../Queue/get-status.md) operation so the asynchronous job can be tracked. Once successfully completed, the server will be restored as specified.

### Entity Definition

| Name |Type | Value | Description |
| --- | --- | --- | --- |
| rel | string | status | The link type |
| href | string | /v2/operations/[ALIAS]/status/[ID] | Address of the job in the queue |
| id | string | [ID] | The identifier of the job in queue. Can be passed to [Get Status](../Queue/get-status.md) call to retrieve status of job. |

### Examples

#### JSON

    {
      "rel":"status",
      "href":"/v2/operations/alias/status/wa1-12345",
      "id":"wa1-12345"
    }
