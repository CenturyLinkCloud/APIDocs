{{{
  "title": "Get Subscriptions",
  "date": "04-05-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Returns a list of all subscriptions and details. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to see all subscriptions and their details. You can narrow focus to a single datacenter and/or subscription status.

## URL

### Structure

    GET https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions?dataCenter={dataCenterId}&status={status}

### Example

    GET https://api.rdbs.ctl.io/v1/ALIAS/subscriptions
    GET https://api.rdbs.ctl.io/v1/ALIAS/subscriptions?dataCenter=UC1
    GET https://api.rdbs.ctl.io/v1/ALIAS/subscriptions?staus=ACTIVE
    GET https://api.rdbs.ctl.io/v1/ALIAS/subscriptions?dataCenter=UC1&staus=PENDING

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account. | Yes |

### Query Parameters

| Name | Type | Description |
| --- | --- | --- |
| dataCenter | string | Short string representing the data center. Datacenters are listed in the `dataCenter` attribute in the RDBS [Get Datacenters](get-datacenters.md) API operation|
| status | string | One of: ACTIVE, BACKING_UP, CONFIGURING, DELETED, FAILED, PENDING, READY, RESTORING, SUCCESS, TERMINATED, UNKNOWN|



## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | number | Subscription id. |
| location | string | Short string representing the data center. Datacenters are listed in the `dataCenter` attribute in the RDBS [Get Datacenters](get-datacenters.md) API operation. |
| instanceType | string | Type of relational database. |
| externalId | string | External id used in connection strings, etc. |
| status | string | One of: Active, Backing Up, Configuring, Deleted, Failed, Pending, Ready, Restoring, Success, Terminated, Unknown. |
| backupTime | string | Scheduled backup time in "hour:minute". |
| backupRetentionDays | string | Number of days to retain backups. |
| servers | array | Servers implementing the subscription. Replicated subscriptions will have two servers. |
| host | string | Host DNS name used in connection strings. |
| port | string | Host port used in connection strings. |
| certificate | string | TLS certificate used to secure subscription connections. |
| backups | array | Database backups available for restore. |


### Server Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | number | Server id. |
| alias | string | Server alias (hostname). |
| location | string | Datacenter id where server is located. |
| cpu | number | Number of CPUs allocated to the server. |
| memory | number | Amount of RAM allocated to the server (GB). |
| storage | number | Amount of disk storage allocated to the server (GB). |
| attributes | object | Misc attributes for the server. |
| connections | number | Estimated number of concurrent connections possible given the server's RAM and CPU. |


### Backup Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | number | Backup id. |
| fileName | string | Backup file name. |
| backupTime | number | Unix timestamp of milliseconds since epoch. |
| backupType | string | One of Automated, Manual.|
| status | string | One of: Active, Backing Up, Configuring, Deleted, Failed, Pending, Ready, Restoring, Success, Terminated, Unknown. |
| size | number | Size of the compressed backup. |


#### JSON

```json
[
  {
    "id": 2957,
    "location": "IL1",
    "instanceType": "MySQL",
    "externalId": "config-db",
    "status": "Active",
    "backupTime": "0:0",
    "backupRetentionDays": 7,
    "servers": [
      {
        "id": 2917,
        "alias": "IL1DBPDMYSQLXXXX",
        "location": "IL1",
        "cpu": 1,
        "memory": 1,
        "storage": 1,
        "attributes": {
          "INTERNAL_IP": "10.90.85.43"
        },
        "connections": 89
      }
    ],
    "host": "config-db.il1.rdbs.ctl.io",
    "port": 49929,
    "certificate": "-----BEGIN CERTIFICATE-----....-----END CERTIFICATE-----",
    "backups": [
      {
        "id": 27538,
        "fileName": "IL1DBPDMYSQLXXXX-2016-03-30_00-00-02.tar.gz",
        "backupTime": 1459296004000,
        "backupType": "Automated",
        "status": "SUCCESS",
        "size": 2841295
      },
      ...
    ]
  },
  ...
```
