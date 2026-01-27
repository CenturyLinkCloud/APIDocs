{{{
  "title": "Get Server Credentials",
  "date": "02-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Retrieves the administrator/root password on an existing server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get the administrator/root password for an existing server.

## URL

### Structure

    GET https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/credentials

### Example

    GET https://api.ctl.io/v2/servers/ACCT/WA1ACCTSERV0101/credentials

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the server with the credentials to return. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| userName | string | The username of root/administrator on the server. Typically "root" for Linux machines and "Administrator" for Windows. |
| password | string | The administrator/root password used to login. |

### Examples

#### JSON

    {
      "userName":"root",
      "password":"P@ssw0rd1"
    }
