{{{
  "title": "Get Policy",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "false"
}}}

Gets the backup policy associated with the specified accountPolicyId. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to retrieve the details of a specific backup policy.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/4ca70660-f08a-407b-830d-e8e9c6c1d59a

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountPolicyId | string | The unique id associated with the backup policy to retrieve | Yes |


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
      "name": "Example Backup Policy",
      "clcAccountAlias": "ACME",
      "status": "ACTIVE",
      "paths": [
        "/var"
      ],
      "excludedDirectoryPaths": [
        "/var/run"
      ],
      "retentionDays": 5,
      "backupIntervalHours": 36,
      "policyId": "4ca70660-f08a-407b-830d-e8e9c6c1d59a"
    }
