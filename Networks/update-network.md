{{{
  "title": "Update Network",
  "date": "5-15-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Updates the attributes of a given Network via PUT. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation to update the name of a network. Users have the option to update the networks' description as well.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly.

## URL

### Structure

    PUT https://api.ctl.io/v2-experimental/networks/{accountAlias}/{dataCenter}/{Network}

### Example

    PUT https://api.ctl.io/v2-experimental/networks/ALIAS/WA1/ec6ff75a0ffd4504840dab343fe41077

## Request

### URI and Querystring Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |
| Network | string | ID of the Network. These can be retrieved from the [Get Network List](../Networks/get-network-list.md) API operation | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| name | string | User-defined name of the network; the default is the VLAN number combined with the network address | Yes |
| description | string | Description of VLAN, a free text field that defaults to the VLAN number combined with the network address | No |

## Examples

### JSON


    {
        "name": "VLAN for Development Servers",
        "description": "Development Servers on 11.22.33.0/24"
    }  

## Response

### Entity Definition

The response will not contain JSON content, but should return the HTTP `200 OK` response upon the successful update of network attributes.
