{{{
  "title": "Add Alert Policy To A Server",
  "date": "03-09-2018",
  "author": "Allen Newton",
  "attachments": []
}}}

Adds an alert policy in a given account to a server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to add a new alert policy within a given account to a server.

## URL

### Structure

    POST https://api.ctl.io/v2/servers/{accountAlias}/{serverId}

### Example

    POST https://api.ctl.io/v2/servers/ALIAS/WA1ACCTWB01

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| ServerId | string | ID of the server for alert policy to be added. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal. | Yes |

### Content Properties

| Name | Type | Description  | Req. |
| --- | --- | --- | --- |
| id | string | Id of the alert policy. | Yes |

### Examples

#### JSON

    {
        "id": "f02f8fbe23a211e8b4670ed5f89f718b"
    }

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the alert policy. |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this policy. |

### Examples

#### JSON

    {
       "id": "f02f8fbe23a211e8b4670ed5f89f718b",
       "links": [
            {
               "rel": "self",
               "href": "/v2/servers/ACCT/WA1ACCTWB01/alertPolicies/f02f8fbe23a211e8b4670ed5f89f718b",
               "verbs": [
                  "DELETE"
               ]
            }
        ]
    }
