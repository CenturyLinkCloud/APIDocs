{{{
  "title": "Get Network List",
  "date": "5-15-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Gets the list of networks available for a given account in a given data center. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need the list of available networks in a given data center you are able to access. Using that list of networks, you can then query for a [specific network](../Networks/get-network.md) in a given data center.

  NOTE: This API operation is experimental only, and not supported for production usage.

## URL

### Structure

    GET https://api.ctl.io/v2-experimental/networks/{accountAlias}/{dataCenter}

### Example

    GET https://api.ctl.io/v2-experimental/networks/ALIAS/WA1

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
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this list of networks |

### Examples

#### JSON

      {
          "id": "711725920a1f4002ac49e634e1789206",
          "cidr": "12.34.0.0/24",
          "description": "vlan_9998_12.34.0",
          "gateway": "12.34.0.1",
          "name": "vlan_9998_12.34.0",
          "netmask": "255.255.255.0",
          "type": "private",
          "vlan": 9998,
          "links": [
              {
                  "rel": "self",
                  "href": "http://api.ctl.io/v2-experimental/networks/ALIAS/WA1/711725920a1f4002ac49e634e1789206",
                  "verbs": [
                      "GET",
                      "PUT"
                  ]
              },
              {
                  "rel": "ipAddresses",
                  "href": "http://api.ctl.io/v2-experimental/networks/ALIAS/WA1/711725920a1f4002ac49e634e1789206/ipAddresses",
                  "verbs": [
                      "GET"
                  ]
              },
              {
                  "rel": "release",
                  "href": "http://api.ctl.io/v2-experimental/networks/ALIAS/WA1/711725920a1f4002ac49e634e1789206/release",
                  "verbs": [
                      "POST"
                  ]
              }
          ]
      },
      {
          "id": "ec6ff75a0ffd4504840dab343fe41077",
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
