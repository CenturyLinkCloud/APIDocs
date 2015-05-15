{{{
  "title": "Update Network",
  "date": "5-15-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Updates the attributes of a given Network via PUT. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you to update the name of a network. Users can optionally update the description.

  NOTE: This API operation is experimental only, and not supported for production usage.

## URL

### Structure

    PUT https://api.ctl.io/v2-experimental/networks/{AccountAlias}/{DataCenter}/{Network}

    {
      "name": "...",  // required
      "description": "..."  // optional
    }

### Example

    PUT https://api.ctl.io/v2-experimental/networks/ALIAS/WA1/ec6ff75a0ffd4504840dab343fe41077

    {
      "name": "VLAN for Development Servers",
      "description": "Development Servers on 11.22.33.0/24"
    }

## Request

### URI and Querystring Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| DataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](get-data-center.md) API operation. | Yes |
| Network | string | ID of the Network. These can be retrieved from the [Get Network List](get-network-list.md) API operation | Yes |

## Response

### Entity Definition

The response will not contain JSON content, but should return the HTTP `200 OK` response upon the update of network attributes.
