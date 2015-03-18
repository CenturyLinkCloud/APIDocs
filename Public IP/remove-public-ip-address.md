{{{
  "title": "Remove Public IP Address",
  "date": "11-23-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Releases the given public IP address of a server so that it is no longer associated with the server and available to be claimed again by another server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to stop using a specific public IP address on an existing server.

## URL

### Structure

    DELETE https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/publicIPAddresses/{publicIP}

### Example

    DELETE https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101/publicIPAddresses/12.34.56.789

## Request

### URI Parameters

|Name|Type|Description|Req.|
|---|---|---|---|
|AccountAlias|string|Short code for a particular account|Yes|
|ServerId|string|ID of the server being queried. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal.|Yes|
|PublicIP|string|The specific public IP to return details about. A server may have more than one public IP, and the list of available ones can be retrieved from the call to [Get Server](../Servers/get-server.md).|Yes|

## Response

The response is a link to the [Get Status](../Queue/get-status.md) operation so the asynchronous job can be tracked. Once successfully completed, the public IP address will no longer be associated with the server.

### Entity Definition

|Name|Type|Value|Description|
|---|---|---|---|
|rel|string|status|The link type|
|href|string|/v2/operations/[ALIAS]/status/[ID]|Address of the job in the queue|
|id|string|[ID]|The identifier of the job in queue. Can be passed to [Get Status](../Queue/get-status.md) call to retrieve status of job.|


### Examples

#### JSON

    {
      "rel":"status",
      "href":"/v2/operations/alias/status/wa1-12345",
      "id":"wa1-12345"
    }
