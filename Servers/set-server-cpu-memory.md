{{{
  "title": "Set Server CPU/Memory",
  "date": "02-11-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes the amount of CPU cores and memory (in GB) on an existing server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the number of CPU cores or the amount of memory for a given server.

## URL

### Structure

    PATCH https://api.ctl.io/v2/servers/{accountAlias}/{serverId}

### Example

    PATCH https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the server with the CPU or memory configuration to update. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |


### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| patchOperation | array | A list of properties, values, and the operations to perform with them for the server. | Yes |

### PatchOperation Definition

| Name | Type | Description |
| --- | --- | --- |
| op | string | The operation to perform on a given property of the server. In this case, the value must be "set" for setting the CPU or memory amount. |
| member | string | The property of the server to perform the operation on. In this case, the value will be either "cpu" or "memory". |
| value | integer | The integer value to set for the given member. For CPU this represents the number of cores; for memory it is in GB. |


### Examples

#### JSON

    [
       {
          "op":"set",
          "member":"cpu",
          "value":"4"
       },
       {
          "op":"set",
          "member":"memory",
          "value":"8"
       }
    ]

## Response

The response is a link to the [Get Status](../Queue/get-status.md) operation so the asynchronous job can be tracked. Once successfully completed, the server configuration will be changed as specified.

### Entity Definition

| Name |Type | Value | Description |
| --- | --- | --- | --- |
| rel | string | status | The link type |
| href | string | /v2/operations/[ALIAS]/status/[ID] | Address of the job in the queue |
| id | string | [ID] | The identifier of the job in queue. Can be passed to [Get Status](../Queue/get-status.md) call to retrieve status of job. |

### Examples

#### JSON

    {
      "rel":"status",
      "href":"/v2/operations/alias/status/wa1-12345",
      "id":"wa1-12345"
    }
