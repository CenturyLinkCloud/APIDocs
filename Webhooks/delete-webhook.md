{{{
  "title": "Delete Webhook",
  "date": "6-23-2016",
  "author": "Marcel Ortiz",
  "attachments": []
}}}

Delete a webhook for an event. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete the webhook for an event.  This will delete all the targetUris for the specified event.

## URL

### Structure

    DELETE https://api.ctl.io/v2/webhooks/{accountAlias}/{event}/configuration

### Example  
    DELETE https://api.ctl.io/v2/webhooks/ALIAS/Account.Created/configuration

## Request

### Uri Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| Event | string | The name of the event for which the webhook will be deleted | Yes |

## Response

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon making the changes successfully.
