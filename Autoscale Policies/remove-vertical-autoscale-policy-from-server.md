{{{
  "title": "Remove Vertical Autoscale Policy from Server",
  "date": "05-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Removes the autoscale policy from a given server, if the policy has first been applied to the server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to remove the autoscale policy from a server.

## URL

### Structure

    DELETE https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/cpuAutoscalePolicy

### Example

    DELETE https://api.ctl.io/v2/servers/ALIAS/WA1ALIASSERV0101/cpuAutoscalePolicy

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| serverId | string | ID of the server. Retrieved from query to containing a group, or by looking at the URL when viewing a server in the Control Portal. | Yes |

## Response

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon deletion of the policy from the server.
