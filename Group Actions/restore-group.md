{{{
  "title": "Restore Group",
  "date": "02-27-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends the restore operation to an archived group. (See [Understanding VM Deployment Options and Power States](http://www.centurylinkcloud.com/knowledge-base/servers/understanding-vm-deployment-options-and-power-states/#archive) for details on the archive operation.) Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.


### When to Use It

Use this API operation when you want to restore an archived group and its groups and servers.

## URL

### Structure

    POST https://api.ctl.io/v2/groups/{accountAlias}/{groupId}/restore

### Example

    POST https://api.ctl.io/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0/restore

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account. | Yes |
| GroupID | string | ID of the group to restore. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| targetGroupId | string | The unique identifier of the target group to restore the group to. | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| isQueued | boolean | Boolean indicating whether the operation was successfully added to the queue. |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this group operation. |
| errorMessage | string | If something goes wrong or the request is not queued, this is the message that contains the details about what happened. |

### Examples

#### JSON

    {
      "isQueued":true,
      "links":[
        {
          "rel":"self",
          "href":"/v2/groups/bryf/2a5c0b9662cf4fc8bf6180f139facdc0?AccountAlias=ALIAS&identifier=2a5c0b9662cf4fc8bf6180f139facdc0"
        },
        {
          "rel":"status",
          "href":"/v2/operations/bryf/status/wa1-12345",
          "id":"wa1-12345"
        }
      ]
    }
