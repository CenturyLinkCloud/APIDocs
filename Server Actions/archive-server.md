{{{
  "title": "Archive Server",
  "date": "02-27-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends the archive operation to a list of servers and adds operation to queue. (See [Understanding VM Deployment Options and Power States](http://www.ctl.io/knowledge-base/servers/understanding-vm-deployment-options-and-power-states/#archive) for details on the archive operation.) Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to archive a single server or group of servers. It should be used in conjunction with the [Get Status](../Queue/get-status.md) operation to check the result of the archive command.

## URL

### Structure

    POST https://api.ctl.io/v2/operations/{accountAlias}/servers/archive

### Example

    POST https://api.ctl.io/v2/operations/ALIAS/servers/archive

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

### Content Properties
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| serverIds | array | List of server IDs to perform archive operation on. | Yes |

### Examples

#### JSON

    [
       "WA1ALIASWB01",
       "WA1ALIASWB02"
    ]

## Response

The response will be an array containing one entity for each server that the operation was performed on.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| server | string | ID of the server that the operation was performed on. |
| isQueued | boolean | Boolean indicating whether the operation was successfully added to the queue. |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this server operation. |
| errorMessage | string | If something goes wrong or the request is not queued, this is the message that contains the details about what happened. |

### Examples

#### JSON

    [
      {
        "server":"wa1aliaswb01",
        "isQueued":true,
        "links":[
          {
            "rel":"status",
            "href":"/v2/operations/alias/status/wa1-12345",
            "id":"wa1-12345"
          }
        ]
      },
      {
        "server":"wa1aliaswb02",
        "isQueued":false,
        "errorMessage":"The operation cannot be queued because the server cannot be found or it is not in a valid state."
      }
    ]
