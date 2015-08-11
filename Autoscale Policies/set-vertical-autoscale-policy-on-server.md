{{{
  "title": "Set Vertical Autoscale Policy on Server",
  "date": "05-25-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sets the autoscale policy for a specified server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to set the autoscale policy of a server.

## URL

### Structure

    PUT https://api.ctl.io/v2/servers/{accountAlias}/{serverId}/cpuAutoscalePolicy

### Example

    PUT https://api.ctl.io/v2/servers/ALIAS/WA1ALIASSERV0101/cpuAutoscalePolicy

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |
| serverId | string | ID of the server. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| id | string | The unique identifier of the autoscale policy to apply to the server. Can be retrieved by calling [Get Vertical Autoscale Policies](../Autoscale Policies/get-vertical-autoscale-policies.md). | Yes |

### Examples

#### JSON
```json
    {
      "id": "3440b69f139c435b8f9462b0661014fc"
    }
```
## Response

### Entity Definition

| Name |Type | Value | Description |
| --- | --- | --- | --- |
| id | string | ID of the autoscale policy. |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this policy. |

### Examples

#### JSON
```json

  {
    "id": "3440b69f139c435b8f9462b0661014fc",
    "links": [
      {
        "rel": "self",
        "href": "/v2/servers/ALIAS/WA1ALIASSERV0101/cpuAutoscalePolicy"
      }
    ]
  }
```
