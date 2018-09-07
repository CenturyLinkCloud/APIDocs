{{{
  "title": "Update Log Forwarding Address",
  "date": "9-7-2018",
  "author": "Matt Peterson",
  "attachments": []
}}}

Updates the network log forwarding configuration for a given data center via PUT. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to update the remote address and protocol used for network log forwarding in a given data center.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly. Only accounts using virtual firewall can use network log forwarding.

## URL

### Structure

    PUT https://api.ctl.io/v2-experimental/networks/{accountAlias}/{dataCenter}/logging

### Example

    PUT https://api.ctl.io/v2-experimental/networks/ALIAS/WA1/logging

## Request

### URI and Querystring Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |

### Content Properties

| Name | Type | Description | Option | Req. |
| --- | --- | --- | --- | --- |
| remoteAddress | string | Address of the remote logging server. If not provided, log forwarding will be disabled for this account | | No |
| protocol | string | Protocol used when sending logs | tcp, udp | Yes |

### Examples

#### JSON
```json
{
    "remoteAddress": "1.2.3.4",
    "protocol": "tcp"
}
```

## Response

The response is an operation used for tracking the status of the new configuration.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| operationID | string | ID used for tracking operation status |
| status | string | Current status of operation |

### Examples

#### JSON
```json
{
    "operationID": "dc5fe58f311f45b3b50de4c9c48ff2e0",
    "status": "pending"
}
```
