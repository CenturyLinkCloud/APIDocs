{{{
  "title": "Delete Server",
  "date": "11-24-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends the delete operation to a given server and adds operation to queue. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete a server that is no longer being used.

## URL

### Structure

    DELETE https://api.ctl.io/v2/servers/{accountAlias}/{serverId}

### Example

    DELETE https://api.ctl.io/v2/servers/ACCT/WA1ACCTWB01

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the server to be deleted. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| server | string | ID of the server that is being deleted. |
| isQueued | boolean | Boolean indicating whether the delete operation was successfully added to the queue. |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this server operation. |
| errorMessage | string | If something goes wrong or the request is not queued, this is the message that contains the details about what happened. |

### Examples

#### JSON

    {
      "server":"wa1acctwb01",
      "isQueued":true,
      "links":[
        {
          "rel":"status",
          "href":"/v2/operations/alias/status/wa1-12345",
          "id":"wa1-12345"
        }
      ]
    }
