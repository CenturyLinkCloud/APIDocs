{{{
  "title": "Add Secondary Network",
  "date": "8-11-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Adds a secondary network adapter to a given server in a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to add a secondary network adapter to a server. You will need a [NetworkId](../Networks/networks-get-network-list.md) to associate with the server. Users have the option to specify an IP address to assign to the server; otherwise the first available IP address in the network will be assigned. Up to four total network adapters can be attached to a server (i.e. a total of 3 secondary adapters). In addition, only one IP address per secondary network can be associated with a server.

## URL

### Structure

    POST https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/networks

### Example

    POST https://api.ctl.io/v2/servers/ALIAS/WA1ALIASSERV0101/networks

## Request

### URI Parameters
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| serverId | string | ID of the server | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| networkId | string | ID of the network. These can be retrieved from the [Get Network List](../Networks/get-network-list.md) API operation | Yes |
| ipAddress | string | Optional IP address for the networkId | No |

### Examples

####JSON
```json
{
      "networkId": "61a7e67908ce4bedabfdaf694a1360fe",
      "ipAddress": "123.456.1.1"
}
```

## Response

The response is a link to the [Get Status](../Queue/get-status.md) operation so the asynchronous job can be tracked. Once successfully completed, the secondary network will be available on the server.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| operationId | string | GUID for the item in the queue for completion |
| uri | string | Link to review status of the operation |

### Examples

#### JSON
```json
  {
    "operationId": "2b70710dba4142dcaf3ab2de68e4f40c",
    "uri": "http://api.ctl.io/v2-experimental/operations/RSDA/status/2b70710dba4142dcaf3ab2de68e4f40c"
  }
```
