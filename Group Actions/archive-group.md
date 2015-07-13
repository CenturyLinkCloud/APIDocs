{{{
  "title": "Archive Group",
  "date": "02-27-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends the archive operation to a group. (See [Understanding VM Deployment Options and Power States](http://www.ctl.io/knowledge-base/servers/understanding-vm-deployment-options-and-power-states/#archive) for details on the archive operation.) Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.


### When to Use It

Use this API operation when you want to archive an entire group and its groups and servers.

## URL

### Structure

    POST https://api.ctl.io/v2/groups/{accountAlias}/{groupId}/archive

### Example

    POST https://api.ctl.io/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0/archive

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account. | Yes |
| GroupID | string | ID of the group to archive. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal. | Yes |

## Response

The response is a link to the [Get Status](../Queue/get-status.md) operation so the asynchronous job can be tracked. Once successfully completed, the group will be archived as specified.

### Entity Definition

| Name | Type | Value | Description |
| --- | --- | --- | --- |
| rel | string | status | The link type |
| href | string | /v2/operations/[ALIAS]/status/[ID]|Address of the job in the queue |
| id | string | [ID]|The identifier of the job in queue. Can be passed to [Get Status](../Queue/get-status.md) call to retrieve status of job. |

### Examples

#### JSON

    {
      "rel":"status",
      "href":"/v2/operations/alias/status/wa1-12345",
      "id":"wa1-12345"
    }
