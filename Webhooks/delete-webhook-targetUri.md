{{{
  "title": "Delete Webhook Target Uri",
  "date": "6-23-2016",
  "author": "Marcel Ortiz",
  "attachments": []
}}}

Delete a target uri from a webhook. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete a single target uri from a particular webhook.

## URL

### Structure
    DELETE https://api.ctl.io/v2/webhooks/{accountAlias}/{event}/configuration/targetUris?targetUri={uri}

### Example  
    DELETE https://api.ctl.io/v2/webhooks/ALIAS/Account.Created/configuration/targetUris?targetUri=https%3A%2F%2Ftest.api%2Faccount%2Fcreated

## Request

### Uri Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| Event | string | The name of the event from which the target uri will be deleted | Yes |
| targetUri | string | The uri that will be removed | Yes |

## Response

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon making the changes successfully.
