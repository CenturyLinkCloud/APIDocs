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

    PUT https://api-va1.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}

### Example

    PUT https://api-va1.backup.ctl.io/clc-backup-api/api/accountPolicies/107e6129-46b6-4b01-afcc-ea733db37214

## Request

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| backupIntervalHours | integer |  | No |
| clcAccountAlias | string |  | No |
| excludedDirectoryPaths | Array[string] |  | No |
| name | string |  | No |
| osType | string | 'Linux' or 'Windows' | No |
| paths | Array[string] |  | No |
| policyId | string |  | No |
| retentionDays | integer |  | No |
| status | string | 'ACTIVE' or 'INACTIVE' | No |

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

### Account Policy Definition

| Name | Type | Description |
| --- | --- | --- |
| backupIntervalHours | integer |  |
| clcAccountAlias | string |  |
| excludedDirectoryPaths | Array[string] |  |
| name | string |  |
| osType | string | 'Linux' or 'Windows' |
| paths | Array[string] |  |
| policyId | string |  |
| retentionDays | integer |  |
| status | string | 'ACTIVE' or 'INACTIVE' |


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

