{{{
  "title": "Claim Network",
  "date": "5-22-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Claims a network for a given account in a given data center. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to claim a network in a given data center you are able to access. Once you have a network, you can then perform various actions like [getting IP addresses](../Networks/get-ip-address-list.md) and [updating its name](../Networks/update-network.md).

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly.

## URL

### Structure

    POST https://api.ctl.io/v2-experimental/networks/{accountAlias}/{dataCenter}/claim

### Example

    POST https://api.ctl.io/v2-experimental/networks/ALIAS/WA1/claim

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
| id | string | ID of the network  |
| cidr | string | The network address, specified using [CIDR notation](http://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) |
| description | string | Description of VLAN, a free text field that defaults to the VLAN number combined with the network address |
| gateway | string | Gateway IP address of the network |
| name | string | User-defined name of the network; the default is the VLAN number combined with the network address |
| netmask | string | A screen of numbers used for routing traffic within a subnet |
| type | string | Network type, usually `private` for networks created by the user |
| vlan | integer | Unique number assigned to the VLAN |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to networks |

### Examples

#### JSON
```json
{
    "id": "e1c1ab9ba070486bbbf114d7bbf556c4",
    "cidr": "11.22.33.0/24",
    "description": "vlan_9999_11.22.33",
    "gateway": "11.22.33.1",
    "name": "vlan_9999_11.22.33",
    "netmask": "255.255.255.0",
    "type": "private",
    "vlan": 9999,
    "links": [
        {
            "rel": "self",
            "href": "http://api.ctl.io/v2-experimental/networks/ALIAS/WA1/e1c1ab9ba070486bbbf114d7bbf556c4",
            "verbs": [
                "GET",
                "PUT"
            ]
        },
        {
            "rel": "ipAddresses",
            "href": "http://api.ctl.io/v2-experimental/networks/ALIAS/WA1/e1c1ab9ba070486bbbf114d7bbf556c4/ipAddresses",
            "verbs": [
                "GET"
            ]
        },
        {
            "rel": "release",
            "href": "http://api.ctl.io/v2-experimental/networks/ALIAS/WA1/e1c1ab9ba070486bbbf114d7bbf556c4/release",
            "verbs": [
                "POST"
            ]
        }
    ]
}
```
