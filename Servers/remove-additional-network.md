{{{
  "title": "Remove Secondary Network",
  "date": "8-11-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Removes a secondary network adapter from a given server in a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to remove a secondary network adapter from a server. You will need a [NetworkId](../Networks/networks-get-network-list) to de-associate with the server.

## URL

### Structure

    DELETE https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/networks/{networkId}

### Example

    DELETE https://api.ctl.io/v2/servers/ALIAS/WA1ALIASSERV0101/networks/478ac773cac24aa7b5e97bac7897fa5a

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
    "operationId": "f0fa5be0ca8e4b3ea182899576fa2c77",
    "uri": "http://api.ctl.io/v2-experimental/operations/ALIAS/status/f0fa5be0ca8e4b3ea182899576fa2c77"
  }
```
