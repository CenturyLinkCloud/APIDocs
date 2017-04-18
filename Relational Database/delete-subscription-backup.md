{{{
  "title": "Delete Subscription Backup",
  "date": "04-13-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Delete a subscription backup. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete a subscription backup. Backup deletion is an asynchronous process; valid requests will be accepted and the delete request queued for further processing.

## URL

### Structure

    DELETE https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}/backups/{backupId}

### Example

    DELETE https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744/backups/2957

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account. | Yes |
| subscriptionId | number | Subscription id. | Yes |
| backupId | number | Backup id. | Yes |

