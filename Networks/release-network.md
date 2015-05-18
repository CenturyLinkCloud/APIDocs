{{{
  "title": "Release Network",
  "date": "5-15-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Releases a network from a given account in a given data center to a pool for another user to claim. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you no longer need a network, and wish to to release it back a given data center.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly.

## URL

### Structure

    POST https://api.ctl.io/v2-experimental/networks/{accountAlias}/{dataCenter}/{Network}/release

### Example

    GET https://api.ctl.io/v2-experimental/networks/ALIAS/WA1/ec6ff75a0ffd4504840dab343fe41077/release

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center you are querying. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |
| Network | string | ID of the Network. This can be retrieved from the [Get Network List](../Networks/get-network-list.md) API operation | Yes |

## Response

### Entity Definition

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon the successful release of the network.
