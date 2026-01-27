{{{
  "title": "Set Maintenance Mode",
  "date": "11-21-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends a specified setting for maintenance mode per server to a list of servers and adds operation to queue. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to explicitly turn on or off maintenance mode on multiple servers. Specifically, this call can be used if you want set some servers to have maintenance mode on and others to have it off. If you want to set maintenance mode for servers to all on or all off, you can use the respective methods for [starting maintenance mode](start-maintenance-mode.md) or [stopping maintenance mode](stop-maintenance-mode.md) for multiple servers.

## URL

### Structure

    POST https://api.ctl.io/v2/operations/{accountAlias}/servers/setMaintenance

### Example

    POST https://api.ctl.io/v2/operations/ALIAS/servers/setMaintenance

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| servers | array | List of server ID and maintenance mode pairs to set. | Yes |

### Servers Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of server to set maintenance mode on or off |
| inMaintenanceMode | boolean | Indicator of whether to place server in maintenance mode or not |

### Examples

#### JSON

    {
      "servers":[
        {
          "id": "wa1aliaswb01",
          "inMaintenanceMode": "true"
        },
        {
          "id": "wa1aliaswb02",
          "inMaintenanceMode": "false"
        }
      ]
    }

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
