{{{
  "title": "Revert to Snapshot",
  "date": "04-22-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Reverts a server to a snapshot. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to revert a server to the state it was in when the given snapshot was taken.

## URL

### Structure

    POST https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/snapshots/{snapshotId}/restore

### Example

    POST https://api.ctl.io/v2/servers/ALIAS/WA1ALIASSERV0101/snapshots/10/restore

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the server with the snapshot to restore. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |
| SnapshotId | string | ID of the snapshot to restore. Retrieved from the `links ` in the `snapshots` section of the [Get Server](../Servers/get-server.md) response. |

## Response

The response is a link to the [Get Status](../Queue/get-status.md) operation so the asynchronous job can be tracked. Once successfully completed, the server snapshot will be  deleted as specified.

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
