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

    GET https://api-va1.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}

### Example

    GET https://api-va1.backup.ctl.io/clc-backup-api/api/accountPolicies/4ca70660-f08a-407b-830d-e8e9c6c1d59a

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountPolicyId | string | The unique id associated with the backup policy to retrieve | Yes |


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
      "name": "Example Backup Policy",
      "clcAccountAlias": "ACME",
      "status": "ACTIVE",
      "paths": [
        "/var"
      ],
      "excludedDirectoryPaths": [],
      "retentionDays": 5,
      "backupIntervalHours": 36,
      "policyId": "4ca70660-f08a-407b-830d-e8e9c6c1d59a"
    }
