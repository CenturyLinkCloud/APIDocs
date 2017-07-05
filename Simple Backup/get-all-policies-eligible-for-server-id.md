{{{
  "title": "Get All Policies Eligible For ServerId",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "false"
}}}

Returns a list of the backup policies that are eligible to be applied to the specified server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to retrieve a list of policies that may be applied to a given server.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/servers/{serverId}

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/servers/VA1ACMEDEMO01

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| serverId | string | Unique server name | Yes |

### QueryString Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| limit | integer | Return up to this many results | No |
| offset | string | Return results starting from this position in the list | No |
| sortBy | string | Sort the results by the specified field | No |
| ascendingSort | boolean | Sort the sortBy field in ascending order | No |

## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| limit | integer | The maximum number of results requested |
| nextOffset | integer | The next position in the list of results for a subsequent call |
| offset | integer | The starting position in the list of results |
| results | Array[Account Policy] | An array of the Policies eligible for the specified server |
| totalCount | integer | The total number of Policies eligible for the specified server |

### Account Policy Definition

| Name | Type | Description |
| --- | --- | --- |
| backupIntervalHours | integer | The backup frequency of the Policy |
| backupSchedule | string | Quartz-flavored CRON string describing the execution schedule for the Policy |
| clcAccountAlias | string | The account alias that the Policy belongs to |
| excludedDirectoryPaths | Array[string] | A list of the directories that the Policy excludes from backup |
| name | string | The name of the Policy |
| osType | string | 'Linux' or 'Windows' |
| paths | Array[string] | A list of the directories that the Policy includes in each backup |
| policyId | string | The unique Id associated with the Policy |
| retentionDays | integer | The number of days backup data will be retained |
| status | string | The status of the backup Policy.  Either 'ACTIVE' or 'INACTIVE'. |


### Examples

#### JSON

    {
      "limit": 2,
      "offset": 0,
      "nextOffset": 2,
      "results": [
        {
          "osType": "Linux",
          "name": "Example Linux Backup Policy 1",
          "clcAccountAlias": "ACME",
          "status": "ACTIVE",
          "paths": [
            "/root"
          ],
          "excludedDirectoryPaths": [],
          "retentionDays": 15,
          "backupIntervalHours": 24,
          "policyId": "284f1801-5f2e-45e0-97d1-a7267ef7a3e8"
        },
        {
          "osType": "Linux",
          "name": "Example Linux Backup Policy 2",
          "clcAccountAlias": "ACME",
          "status": "ACTIVE",
          "paths": [
            "/opt"
          ],
          "excludedDirectoryPaths": [],
          "retentionDays": 7,
          "backupSchedule": "0 0 12 ? * SUN *",
          "policyId": "18b4bdd3-cbdf-40c5-86bf-3c36b0a060f5"
        }
      ],
      "totalCount": 2
    }
