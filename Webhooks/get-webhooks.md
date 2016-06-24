{{{
  "title": "Get Webhooks",
  "date": "6-23-2016",
  "author": "Marcel Ortiz",
  "attachments": []
}}}

Gets the details on the configured webhooks. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to discover all the webhooks that have been configured for every available event and get links to operations for modifying those webhooks.

## URL

### Structure

    GET https://api.ctl.io/v2/webhooks/{accountAlias}

### Example  
    GET https://api.ctl.io/v2/webhooks/ALIAS

## Request

### Uri Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |


## Response

### Webhook Collection Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| items | Webhook[] | A list of webhooks, one per available event |

### Webhook Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| name | string | The name of the event that triggers the webhook |
| configuration | Configuration | Details about the webhook handling the event |

### Configuration Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| recursive | boolean | If true, the webhook will be called when the event occurs in a sub-accounts |
| targetUris | TargetUri[] | The list of targets to be called when the event occurs |


### TargetUri Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| targetUri | string | A uri that will be called when the event occurs |

### Examples

#### JSON

    {
      "items": [
        {
          "name": "Account.Created",
          "configuration": {
            "recursive": false,
            "targetUris": [
              {
                "targetUri": "https://uri.test/account/created"
              },
              {
                "targetUri": "https://api.test/account/created"
              }
            ]
          },
          "links": [
            {
              "rel": "configuration",
              "href": "/v2/webhooks/RJP/Account.Created/configuration",
              "verbs": [
                "DELETE",
                "PUT"
              ]
            }
          ]
        },
        {
          "name": "Account.Deleted",
          "configuration": {
            "recursive": false,
            "targetUris": [
              {
                "targetUri": "https://api.test/account/deleted"
              }
            ]
          },
          "links": [
            {
              "rel": "configuration",
              "href": "/v2/webhooks/RJP/Account.Deleted/configuration",
              "verbs": [
                "DELETE",
                "PUT"
              ]
            }
          ]
        },
        {
          "name": "Account.Updated",
          "links": [
            {
              "rel": "configuration",
              "href": "/v2/webhooks/RJP/Account.Updated/configuration",
              "verbs": [
                "DELETE",
                "PUT"
              ]
            }
          ]
        },
        {
          "name": "Alert.Notification",
          "links": [
            {
              "rel": "configuration",
              "href": "/v2/webhooks/RJP/Alert.Notification/configuration",
              "verbs": [
                "DELETE",
                "PUT"
              ]
            }
          ]
        },
        {
          "name": "Server.Created",
          "links": [
            {
              "rel": "configuration",
              "href": "/v2/webhooks/RJP/Server.Created/configuration",
              "verbs": [
                "DELETE",
                "PUT"
              ]
            }
          ]
        },
        {
          "name": "Server.Deleted",
          "links": [
            {
              "rel": "configuration",
              "href": "/v2/webhooks/RJP/Server.Deleted/configuration",
              "verbs": [
                "DELETE",
                "PUT"
              ]
            }
          ]
        },
        {
          "name": "Server.Updated",
          "links": [
            {
              "rel": "configuration",
              "href": "/v2/webhooks/RJP/Server.Updated/configuration",
              "verbs": [
                "DELETE",
                "PUT"
              ]
            }
          ]
        },
        {
          "name": "User.Created",
          "links": [
            {
              "rel": "configuration",
              "href": "/v2/webhooks/RJP/User.Created/configuration",
              "verbs": [
                "DELETE",
                "PUT"
              ]
            }
          ]
        },
        {
          "name": "User.Deleted",
          "links": [
            {
              "rel": "configuration",
              "href": "/v2/webhooks/RJP/User.Deleted/configuration",
              "verbs": [
                "DELETE",
                "PUT"
              ]
            }
          ]
        },
        {
          "name": "User.Updated",
          "links": [
            {
              "rel": "configuration",
              "href": "/v2/webhooks/RJP/User.Updated/configuration",
              "verbs": [
                "DELETE",
                "PUT"
              ]
            }
          ]
        }
      ],
      "links": [
        {
          "rel": "self",
          "href": "/v2/webhooks/RJP"
        }
      ]
    }
