{{{
  "title": "Set Webhook",
  "date": "6-23-2016",
  "author": "Marcel Ortiz",
  "attachments": []
}}}

Change the configuration of a webhook for a specific event. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the configuration of a webhook including the uris that get called when the event occurs and whether the uris are called when the event occurs in a sub-account.

## URL

### Structure

    PUT https://api.ctl.io/v2/webhooks/{accountAlias}/{event}/configuration

### Example  
    PUT https://api.ctl.io/v2/webhooks/ALIAS/Account.Created/configuration

## Request

### Uri Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| Event | string | The name of the webhook event being configured | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| recursive | string | If true, the webhook is called when the event occurs in sub-accounts | Yes |
| targetUris | TargetUri[] | The targets called when the event occurs | No |

#### TargetUri Entity Definition

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| targetUri | string | A uri that will be called when the event occurs | Yes |

### Examples

#### JSON

    {
      recursive: true,
      targetUris: [
        { targetUri: "https://test.uri/account/created" },
        { targetUri: "https://test.api" }
      ]
    }

## Response

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon making the changes successfully.
