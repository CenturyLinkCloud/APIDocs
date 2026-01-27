{{{
  "title": "Execute Package",
  "date": "11-21-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Executes a single package on one or more servers. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to execute a Blueprint package that is available from within a given account on one or more servers. The list of available packages can be retrieved from the __Get Packages__ API operation.

## URL

### Structure

    POST https://api.ctl.io/v2/operations/{accountAlias}/servers/executePackage

### Example

    POST https://api.ctl.io/v2/operations/ALIAS/servers/executePackage

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| servers | array | List of server IDs to run the package on. | Yes |
| package | complex | The package entity describing which package to run on the specified servers. | Yes |

### Package Definition

| Name | Type | Description |
| --- | --- | --- |
| packageId | string | Unique identifier of the package to execute. |
| parameters | complex | Set of key-value pairs for setting the package-specific parameters defined. |

### Examples

#### JSON

    {
        "servers": [
            "wa1aliaswb01"
        ],
        "package": {
            "packageId": "86567681-c79c-1234-a530-850708435c23",
            "parameters": {
                "AB.HelloWorld.Variable": "someValue"
            }
        }
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
      }
    ]
