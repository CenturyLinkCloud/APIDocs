{{{
  "title": "Get Log Forwarding Address",
  "date": "9-7-2018",
  "author": "Matt Peterson",
  "attachments": []
}}}

Gets the current configuration for network log forwarding. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need the address and protocol currently configured for network log forwarding.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly. Only accounts using virtual firewall can use network log forwarding.

## URL

### Structure

    GET https://api.ctl.io/v2-experimental/networks/{accountAlias}/{dataCenter}/logging

### Example

    GET https://api.ctl.io/v2-experimental/networks/ALIAS/WA1/logging

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| remoteAddress | string | Address of the remote logging server |
| protocol | string | Protocol used when sending logs |

### Examples

#### JSON
```json
{
    "remoteAddress": "1.2.3.4",
    "protocol": "tcp"
}
```
