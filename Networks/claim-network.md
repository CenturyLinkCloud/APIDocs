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

## Response [UPDATED JANUARY 6 2016]

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to networks. |

### Examples

#### JSON
```
  {
    "rel": "status",

    "href": "/v2/operations/qcp/status/wa1-91567",

    "id": "wa1-91567"

  }
```

NOTE: To get the status of the "claim network" operation, query the `href` in the response. To do this, follow these steps:

1. Login to the Control Portal.
2. Split the location (characters before the `-` in the id), and the numbers after the `-`), and enter them into the address bar of your browser in the following format: `https://control.ctl.io/Blueprints/Queue/RequestDetails/91567?location=wa1`
3. The response at this URL will then provide status details, but no information about the network itself.
