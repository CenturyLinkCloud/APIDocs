{{{
  "title": "Create Subscription",
  "date": "04-05-2015",
  "author": "Relational Database Services",
  "attachments": []
}}}

Create a new subscription. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new subscription.

## URL

### Structure

    POST https://api.rdbs.ctl.io/v1/{accountAlias}/subscriptions

### Example

    POST https://api.rdbs.ctl.io/v1/ALIAS/subscriptions

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountAlias | string | Short code for a particular account | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| instanceType | string | One of MYSQL, MySQL_REPLICATION | Yes |
| location | string | Datacenter id. Available datacenters are listed in [Get Datacenters method](get-datacenters.md) | Yes |
| externalId | string | The hostname part of the connection string | Yes |
| machineConfig | Object | Server provisioning information for cpu, memory, and storage | Yes |
| backupRetentionDays | number | Number of days to retain database backups | Yes |
| destinations | array | Server capacity notification destinations | No |
| users | array | Initial database user account. | Yes |
| backupTime | object | Time of day to run backups (UTC) | Yes |


### MachineConfig Definition

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| cpu | number | Number of CPUs to allocate to server | Yes |
| memory | number | Amount of RAM to allocate to server (GB) | Yes |
| storage | number | Amount of disk storage to allocate to server (GB) | Yes |

### Destination Definition

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| destinationType | string | EMAIL | Yes |
| location | string | Where to send notifications. For EMAIL, this is an email address. | Yes |
| notifications | array | A list of notifications to receive. | Yes |

### Notification Definition

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| notificationType | string | One of CPU_UTILIZATION, MEMORY_UTILIZATION, STORAGE_UTILIZATION | Yes |

### User Definition

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| name | string | User name. | Yes |
| password | string | User password. The password must pass our minimum requirements: at least 9 characters and contain at least 3 of the following: uppercase letters, lowercase letters, numbers, symbols| Yes |

### BackupTime Definition

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| hour | number | Hour of day to start backup (UTC). | Yes |
| minute | number | Minute of minute to start backup (UTC). | Yes |

### Example

```json
{
  "instanceType": "MySQL",
  "location": "VA1",
  "externalId": "st-api-test",
  "machineConfig": {
    "cpu": 1,
    "memory": 1,
    "storage": 1
  },
  "backupRetentionDays": 7,
  "destinations": [
    {
      "destinationType": "EMAIL",
      "location": "foo@bar.com",
      "notifications": [
        {
          "notificationType": "CPU_UTILIZATION"
        },
        {
          "notificationType": "MEMORY_UTILIZATION"
        }
      ]
    }
  ],
  "users": [
   {
     "name": "admin",
     "password": "AstrongPW!"
   }
  ],
  "backupTime": {
    "hour": 9,
    "minute": 15
  }
}
```


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | number | Subscription id |
| location | string | Datacenter id |
| instanceType | string | Type of relational database. |
| externalId | string | External id used in connection strings, etc. |
| status | string | One of: Active, Backing Up, Configuring, Deleted, Failed, Pending, Ready, Restoring, Success, Terminated, Unknown |
| backupTime | string | Scheduled backup time in "hour:minute" |
| backupRetentionDays | string | Number of days to retain backups. |
| servers | array | Servers implementing the subscription. Replicated subscriptions will have two servers. |
| host | string | Host DNS name used in connection strings. |
| port | string | Host port used in connection strings. |
| certificate | string | TLS certificate used to secure subscription connections. |

### Server Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | number | Server id |
| alias | string | Server alias (hostname) |
| location | string | Datacenter id where server is located |
| cpu | number | Number of CPUs allocated to the server |
| memory | number | Amount of RAM allocated to the server (GB) |
| storage | number | Amount of disk storage allocated to the server (GB) |
| attributes | object | Misc attributes for the server |
| connections | number | Estimated number of concurrent connections possible given the server's RAM and CPU. |


#### JSON

```json
{
  "id": 894,
  "location": "VA1",
  "instanceType": "MySQL",
  "externalId": "st-api-test",
  "status": "Configuring",
  "backupTime": "9:15",
  "backupRetentionDays": 6,
  "servers": [
    {
      "id": 1025,
      "alias": "VA1DBDVMYSQL2130",
      "location": "va1",
      "cpu": 1,
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
