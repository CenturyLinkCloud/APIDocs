{{{
  "title": "Remove Secondary Network",
  "date": "8-11-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Removes a secondary network adapter from a given server in a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to remove a secondary network adapter from a server. You will need a [NetworkId](../Networks/networks-get-network-list.md) to de-associate with the server.

## URL

### Structure

    DELETE https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/networks/{networkId}

### Example

    DELETE https://api.ctl.io/v2/servers/ALIAS/WA1ALIASSERV0101/networks/f49875b17cee4b8c99bf1ab75aa286d6

## Request

### URI Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| serverId | string | ID of the server | Yes |
| networkId | string | ID of the network. These can be retrieved from the [Get Network List](../Networks/get-network-list.md) API operation | Yes |

## Response

The response is a link to the [Get Status](../Queue/get-status.md) operation so the asynchronous job can be tracked. Once successfully completed, the secondary network will be removed from the server.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| operationId | string | GUID for the item in the queue for completion |
| uri | string | Link to review status of the operation |

### Examples

#### JSON
```json
  {
    "operationId": "6c8d7b5349054fe6a532539ff066b53b",
    "uri": "http://api.ctl.io/v2-experimental/operations/ALIAS/status/6c8d7b5349054fe6a532539ff066b53b"
  }
```
