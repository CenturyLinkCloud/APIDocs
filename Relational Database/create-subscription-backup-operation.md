{{{
  "title": "Create Subscription Backup Operation",
  "date": "04-13-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Initiation a subscription backup's operation. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to restore a subscription's backup. You may restore a backup to the subscription it was created from, or to another subscription with equal or greater storage. Backup restore is an asynchronous process; valid requests will be accepted and the restore request queued for further processing.

## URL

### Structure

    POST https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}/backups/{backupId}/operations

### Example

    POST https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744/backups/2957/operations

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account. | Yes |
| subscriptionId | number | Subscription id. | Yes |
| backupId | number | Backup id. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| type | string | 'restore' | Yes |
| toSubscriptionId | number | The id of the subscription you want to restore this backup to. The target subscription may be any subscription in your account that has equal or greater storage. | Yes |

