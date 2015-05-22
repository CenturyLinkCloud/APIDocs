{{{
  "title": "Get Network",
  "date": "5-22-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Gets the details of a specific network in a given data center for a given account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to discover properties of a network in a data center. You may optionally query details of IP Addresses on this network.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly.

## URL

### Structure

    GET https://api.ctl.io/v2-experimental/networks/{accountAlias}/{dataCenter}/{Network}?ipAddresses=none|claimed|free|all

### Example

    GET https://api.ctl.io/v2-experimental/networks/ALIAS/WA1/ec6ff75a0ffd4504840dab343fe41077?ipAddresses=claimed

## Request

### URI and Querystring Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |
| Network | string | ID of the Network. This can be retrieved from the [Get Network List](../Networks/get-network-list.md) API operation. | Yes |
| ipAddresses | string | Optional component of the query to request details of IP Addresses in a certain state. Should be one of the following: "none" (returns defaults on the network only), "claimed" (returns details of the network as well as information about claimed IP addresses), "free" (returns details of the network as well as information about free IP addresses) or "all" (returns details of the network as well as information about all IP addresses). Refer to [Get IP Address List](../Networks/get-ip-address-list.md) for the data shape of returned IP addresses. | No |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the network  |
| cidr | string | The network address, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) |
| description | string | Description of VLAN, a free text field that defaults to the VLAN number combined with the network address |
| gateway | string | Gateway IP address of the network |
| name | string | User-defined name of the network; the default is the VLAN number combined with the network address |
| netmask | string | A screen of numbers used for routing traffic within a subnet |
| type | boolean | Network type, usually `private` for networks created by the user |
| vlan | integer| Unique number assigned to the VLAN |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this list of networks |

### Examples

#### JSON
```json
{
    "id": "ec6ff75a0ffd4504840dab343fe41077",
    "cidr": "11.22.33.0/24",
    "description": "vlan_9999_11.22.33",
    "gateway": "11.22.33.1",
    "name": "vlan_9999_11.22.33",
    "netmask": "255.255.255.0",
    "type": "private",
    "vlan": 9999,
    "ipAddresses": [
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
            "address": "65.43.210.123",
            "claimed": true,
            "server": "WA1ALIASAPI01",
            "type": "publicMapped"
        }
    ],
    "links": [
        {
            "rel": "self",
            "href": "http://api.ctl.io/v2-experimental/networks/ALIAS/WA1/ec6ff75a0ffd4504840dab343fe41077",
            "verbs": [
                "GET",
                "PUT"
            ]
        },
        {
            "rel": "ipAddresses",
            "href": "http://api.ctl.io/v2-experimental/networks/ALIAS/WA1/ec6ff75a0ffd4504840dab343fe41077/ipAddresses",
            "verbs": [
                "GET"
            ]
        },
        {
            "rel": "release",
            "href": "http://api.ctl.io/v2-experimental/networks/ALIAS/WA1/ec6ff75a0ffd4504840dab343fe41077/release",
            "verbs": [
                "POST"
            ]
        }
    ]
}
```
