{{{
  "title": "Create Policy",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "true"
}}}

Creates a new backup policy associated with the account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new backup policy.

## URL

### Structure

    POST https://api-va1.backup.ctl.io/clc-backup-api/api/accountPolicies

### Example

    POST https://api-va1.backup.ctl.io/clc-backup-api/api/accountPolicies

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
      "status": "ACTIVE",
      "paths": [
        "/opt"
      ],
      "retentionDays": 7,
      "backupIntervalHours": 12
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
        "/opt"
      ],
      "excludedDirectoryPaths": [],
      "retentionDays": 7,
      "backupIntervalHours": 12,
      "policyId": "107e6129-46b6-4b01-afcc-ea733db37214"
    }
