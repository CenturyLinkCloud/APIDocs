{{{
  "title": "Patch Subscription",
  "date": "04-08-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Modify an existing subscription. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to resize a subscription server(s), change the number of days to keep backups, or the backup time.

**NOTE**: A subscription storage allocation cannot be reduced.

## URL

### Structure

    PATCH https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions/{subscriptionId}

### Example

    PATCH https://api.rdbs.ctl.io/v1/ALIAS/subscriptions/744

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account. | Yes |
| subscriptionId | number | Subscription id. | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| machineConfig | Object | Server provisioning information for cpu, memory, and storage. | Yes |
| backupRetentionDays | number | Number of days to retain database backups. | Yes |
| backupTime | object | Time of day to run backups (UTC). | Yes |


### MachineConfig Definition

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| cpu | number | Number of CPUs to allocate to server. | Yes |
| memory | number | Amount of RAM to allocate to server (GB). | Yes |
| storage | number | Amount of disk storage to allocate to server (GB). | Yes |

### BackupTime Definition

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| hour | number | Hour of day to start backup (UTC). | Yes |
| minute | number | Minute of minute to start backup (UTC). | Yes |

### Example

```json
{
  "machineConfig": {
    "cpu": 2,
    "memory": 1,
    "storage": 1
  },
  "backupRetentionDays": 6,
  "backupTime": {
    "hour": 1,
    "minute": 15
  }
}
```

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


#### JSON

```json
{
  "id": 894,
  "location": "VA1",
  "instanceType": "MySQL",
  "externalId": "st-api-test",
  "status": "Configuring",
  "backupTime": "1:15",
  "backupRetentionDays": 6,
  "servers": [
    {
      "id": 1025,
      "alias": "VA1DBDVMYSQL2130",
      "location": "va1",
      "cpu": 2,
      "memory": 1,
      "storage": 1,
      "attributes": {
        "INTERNAL_IP": "10.126.63.89"
      },
      "connections": 89
    }
  ],
  "host": "10.126.63.31",
  "port": 49562,
  "certificate": "-----BEGIN CERTIFICATE-----....-----END CERTIFICATE-----"
}}
```
