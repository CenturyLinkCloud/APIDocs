{{{
  "title": "Delete Group",
  "date": "11-24-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends the delete operation to a given group and adds operation to queue. This operation will delete the group and all servers and groups underneath it. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete a group and all objects underneath it.

## URL

### Structure

    DELETE https://api.ctl.io/v2/groups/{accountAlias}/{groupId}

### Example

    DELETE https://api.ctl.io/v2/servers/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| GroupId | string | ID of the group to be deleted. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal. | Yes |

## Response

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
