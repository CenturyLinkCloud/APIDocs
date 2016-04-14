{{{
  "title": "Get Subscription Backups",
  "date": "04-13-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Returns details of subscription backups. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to see a subscription's backups. 

## URL

### Structure

    GET https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}/backups

### Example

    GET https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744/backups

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account. | Yes |
| subscriptionId | number | Subscription id. | Yes |


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | number | Backup id. |
| fileName | string | Backup file name. |
| backupTime | number | Unix timestamp of milliseconds since epoch. |
| backupType | string | One of Automated, Manual .|
| status | string | One of: Active, Backing Up, Configuring, Deleted, Failed, Pending, Ready, Restoring, Success, Terminated, Unknown. |
| size | number | Size of the compressed backup. |


#### JSON

```json
[
  {
    "id": 2656,
    "fileName": "UC1DBDVMYSQL566-2016-04-06_23-00-01.tar.gz",
    "backupTime": 1459983603000,
    "backupType": "Automated",
    "status": "SUCCESS",
    "size": 2842348
  },
  {
    "id": 2674,
    "fileName": "UC1DBDVMYSQL566-2016-04-07_23-00-01.tar.gz",
    "backupTime": 1460070003000,
    "backupType": "Automated",
    "status": "SUCCESS",
    "size": 2842335
  },
  ...
}
```
