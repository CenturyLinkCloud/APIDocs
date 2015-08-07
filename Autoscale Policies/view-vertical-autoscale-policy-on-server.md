{{{
  "title": "View Vertical Autoscale Policy on Server",
  "date": "05-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Gets the autoscale policy of a given server, if a policy has been applied on the server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get the autoscale policy of a given server.

## URL

### Structure

    GET https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/cpuAutoscalePolicy

### Example

    GET https://api.ctl.io/v2/servers/ALIAS/WA1ALIASSERV0101/cpuAutoscalePolicy

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| serverId | string | ID of the server. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |

## Response

### Entity Definition

| Name |Type | Value | Description |
| --- | --- | --- | --- |
| id | string | ID of the autoscale policy |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this policy |

### Examples

#### JSON
```json
  {
    "id": "6c8d7b5349054fe6a532539ff066b53b",
    "links": [
      {
        "rel": "self",
        "href": "/v2/servers/ALIAS/WA1ALIASSERV0101/cpuAutoscalePolicy"
      }
    ]
  }
```
