{{{
  "title": "Add Webhook Target Uri",
  "date": "6-23-2016",
  "author": "Marcel Ortiz",
  "attachments": []
}}}

Add a target uri to the webhook for a specified event. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to add a uri to the collection of targetUris in a webhook.

## URL

### Structure

    POST https://api.ctl.io/v2/webhooks/{accountAlias}/{event}/configuration/targetUris

### Example  
    POST https://api.ctl.io/v2/webhooks/ALIAS/Account.Created/configuration/targetUris

## Request

### Uri Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| Event | string | The name of the webhook event being configured | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| targetUri | string | A uri that will be called when the event occurs | Yes |

### Examples

#### JSON
    { targetUri: "https://test.api/account/created" }

## Response

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon making the changes successfully.
