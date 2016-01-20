{{{
  "title": "Claim Network",
  "date": "1-5-2016",
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

## Response [UPDATED JANUARY 19 2016]

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| operationId | string | Unique identifier for network claim operation |
| uri | string | URI to check status of operation |

### Examples

#### Initial Response Example

The initial response from the Claim Network API provides the unique identifier for the asynchronous operation to claim the network and a URI to check the status of that operation.

```
{
  "operationId": "c387aa9873ab4f7399ea8964dd61510d",
  "uri": "/v2-experimental/operations/{accountAlias}/status/{operationId}"
}
```

While the operation is executing, the response from the operation URI will provide a summary of the operation.

```
{
  "requestType": "blueprintOperation",
  "status": "running",
  "summary": {
    "blueprintId": 92121,
    "locationId": "{locationAlias}"
  },
  "source": {
    "userName": "{requestedUser}",
    "requestedAt": "2016-01-11T18:39:07Z"
  }
}
```

When the operation completes successfully the response will provide a status property as "succeeded" and a link to the claimed network.

```
{
  "requestType": "blueprintOperation",
  "status": "succeeded",
  "summary": {
    "blueprintId": 92121,
    "locationId": "{locationAlias}",
    "links": [
      {
        "rel": "network",
        "href": "/v2-experimental/networks/{accountAlias}/{locationAlias}/{networkId}",
        "id": "{networkId}"
      }
    ]
  },
  "source": {
    "userName": "{requestedUser}",
    "requestedAt": "2016-01-11T18:39:07Z"
  }
}
```

If the operation to claim a network were to fail, the response will come back with status "failed" along with the operation summary information.

```
{
  "requestType": "blueprintOperation",
  "status": "failed",
  "summary": {
    "blueprintId": 92123,
    "locationId": "{locationId}"
  },
  "source": {
    "userName": "{requestedUser}",
    "requestedAt": "2016-01-11T18:43:42Z"
  }
}
```