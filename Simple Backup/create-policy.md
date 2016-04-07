{{{
  "title": "Create Policy",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "true"
}}}

Creates a new backup policy associated with the account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a brand new backup policy.

## URL

### Structure

    POST https://api.backup.ctl.io/clc-backup-api/api/accountPolicies

### Example

    POST https://api.backup.ctl.io/clc-backup-api/api/accountPolicies

## Request

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| backupIntervalHours | integer | The backup frequency of the Policy specified in hours | Yes |
| clcAccountAlias | string | The account alias that the Policy belongs to | No |
| excludedDirectoryPaths | Array[string] | A list of the directories that the Policy excludes from backup | No |
| name | string | The name of the Policy | Yes |
| osType | string | 'Linux' or 'Windows' | Yes |
| paths | Array[string] | A list of the directories that the Policy includes in each backup | Yes |
| retentionDays | integer | The number of days backup data will be retained | Yes |

### Examples

#### JSON

    {
      "osType": "Linux",
      "name": "Example Backup Policy from API",
      "paths": [
        "/opt"
      ],
      "retentionDays": 7,
      "backupIntervalHours": 12
    }


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| backupIntervalHours | integer | The backup frequency of the Policy |
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
      "osType": "Linux",
      "name": "Example Backup Policy from API",
      "clcAccountAlias": "ACME",
      "status": "ACTIVE",
      "paths": [
        "/opt"
      ],
      "excludedDirectoryPaths": [],
      "retentionDays": 7,
      "backupIntervalHours": 12,
      "policyId": "107e6129-46b6-4b01-afcc-ea733db37214"
    }
