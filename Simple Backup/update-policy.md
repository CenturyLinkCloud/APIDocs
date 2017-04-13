{{{
  "title": "Update Policy",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "false"
}}}

Updates a backup policy. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to change the settings of a backup policy. It can be used to modify the name, frequency, paths to include, and paths to exclude.  Operating System and Retention may not be modified.

## URL

### Structure

    PUT https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}

### Example

    PUT https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/107e6129-46b6-4b01-afcc-ea733db37214

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountPolicyId | string | The unique id associated with the backup policy to update | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| backupIntervalHours | integer | The backup frequency of the Policy specified in hours | Yes |
| excludedDirectoryPaths | Array[string] | A list of the directories that the Policy excludes from backup | Yes |
| name | string | The name of the Policy | Yes |
| osType | string | 'Linux' or 'Windows' | Yes |
| paths | Array[string] | A list of the directories that the Policy includes in each backup | Yes |
| policyId | string | The unique Id associated with the Policy | Yes |
| retentionDays | integer | The number of days backup data will be retained | Yes |
| status | string | 'ACTIVE' or 'INACTIVE' | Yes |

### Examples

#### JSON

    {
      "osType": "Linux",
      "name": "Example Backup Policy from API",
      "clcAccountAlias": "ACME",
      "status": "ACTIVE",
      "paths": [
        "/var",
        "/srv",
        "/etc",
        "/home",
        "/usr"
      ],
      "excludedDirectoryPaths": [
        "/var/run",
        "/var/cache",
        "/var/tmp"
      ],
      "retentionDays": 7,
      "backupIntervalHours": 12,
      "policyId": "107e6129-46b6-4b01-afcc-ea733db37214"
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
        "/var",
        "/srv",
        "/etc",
        "/home",
        "/usr"
      ],
      "excludedDirectoryPaths": [
        "/var/run",
        "/var/cache",
        "/var/tmp"
      ],
      "retentionDays": 7,
      "backupIntervalHours": 12,
      "policyId": "107e6129-46b6-4b01-afcc-ea733db37214"
    }

