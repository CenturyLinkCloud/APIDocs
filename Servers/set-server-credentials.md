{{{
  "title": "Set Server Credentials",
  "date": "02-10-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Changes the administrator/root password on an existing server given the current administrator/root password. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the administrator/root password on an existing server.

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
| ServerId | string | ID of the server with the credentials to update. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |


### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| patchOperation | array | A list of properties, values, and the operations to perform with them for the server. | Yes |

### PatchOperation Definition

| Name | Type | Description |
| --- | --- | --- |
| op | string | The operation to perform on a given property of the server. In this case, the value must be "set" for setting the credentials. |
| member | string | The property of the server to perform the operation on. In this case, the value must be "password" for setting the credentials. |
| value | complex | The current and new administrator/root password values. |

### Value Definition

| Name | Type | Description |
| --- | --- | --- |
| current | string | The current administrator/root password used to login. |
| password | string | The new administrator/root password to change to. |


### Examples

#### JSON

    [
       {
          "op":"set",
          "member":"password",
          "value":
          {
             "current":"OldP@ssw0rd1",
             "password":"NewP@ssw0rd2"
          }
       }
    ]

## Response

The response is a link to the [Get Status](../Queue/get-status.md) operation so the asynchronous job can be tracked. Once successfully completed, the password will be changed as specified.

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
