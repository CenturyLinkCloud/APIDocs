{{{
  "title": "Clone Server",
  "date": "04-22-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Creates a new server as a clone of an existing server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new server from a standard or custom template, or clone an existing server.

## URL

### Structure

    POST https://api.ctl.io/v2/servers/{accountAlias}

### Example

    POST https://api.ctl.io/v2/servers/ALIAS/

## Request

The request parameters are the same as defined for [Create Server](create-server.md) with the addition of the `sourceServerPassword` parameter being required when cloning a server. Also, note that the `sourceServerId` paramater should be the name of the server that is being cloned rather than a template name.

### Examples

#### JSON

    {
      "name": "web",
      "groupId": "2a5c0b9662cf4fc8bf6180f139facdc0",
      "sourceServerId": "WA1ALIASWEB01",
      "sourceServerPassword": "P@ssw0rd1",
      "cpu": 2,
      "memoryGB": 4,
      "type": "standard"
    }

## Response

The response will be the same as specified in [Create Server](create-server.md).
