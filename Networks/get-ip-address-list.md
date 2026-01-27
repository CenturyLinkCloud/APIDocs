{{{
  "title": "Get IP Address List",
  "date": "5-22-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Gets the list of IP addresses for a network in a given data center for a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need the list of IP Addresses associated with a given network.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly.

## URL

### Structure

    GET https://api.ctl.io/v2-experimental/networks/{accountAlias}/{dataCenter}/{Network}/ipAddresses?type=claimed|free|all

### Example

    GET https://api.ctl.io/v2-experimental/networks/ALIAS/WA1/ec6ff75a0ffd4504840dab343fe41077/ipAddresses?type=claimed

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |
| Network | string | ID of the Network. These can be retrieved from the [Get Network List](../Networks/get-network-list.md) API operation | Yes |
| type | string | Optional component of the query to request details of IP Addresses in a certain state. Should be one of the following: "claimed" (returns details of the network as well as information about claimed IP addresses), "free" (returns details of the network as well as information about free IP addresses) or "all" (returns details of the network as well as information about all IP addresses) | No |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| address | string | An IP Address on the Network |
| claimed | boolean | Indicates claimed status of the address, either `true` or `false` |
| server | string | ID of the server associated with the IP address, if claimed |
| type | string | Indicates if the IP address is `private`, `publicMapped`, or `virtual` |

### Examples

#### JSON
```json
[
    {
        "address": "11.22.33.12",
        "claimed": true,
        "server": "WA1ALIASAPI01",
        "type": "private"
    },
    {
        "address": "11.22.33.13",
        "claimed": true,
        "server": "WA1ALIASAPI01",
        "type": "private"
    },
    {
        "address": "11.22.33.14",
        "claimed": false,
        "type": "private"
    },
    {
        "address": "65.43.210.123",
        "claimed": true,
        "server": "WA1ALIASAPI01",
        "type": "publicMapped"
    }
]
```
