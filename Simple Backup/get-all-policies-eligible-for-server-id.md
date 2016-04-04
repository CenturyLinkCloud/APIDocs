{{{
  "title": "Get All Policies Eligible For ServerId",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "false"
}}}

Returns a list of the backup policies that are eligible to be applied to the specified server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to . It can be used to .

## URL

### Structure

    GET https://api-va1.backup.ctl.io/clc-backup-api/servers/{serverId}

### Example

    GET https://api-va1.backup.ctl.io/clc-backup-api/servers/VA1ACMEDEMO01

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| limit | integer |  | No |
| offset | string |  | No |
| sortBy | string |  | No |
| ascendingSort | boolean | Sort the sortBy field in ascending order | No |

## Response

### Account Policies Definition

| Name | Type | Description |
| --- | --- | --- |
| limit | integer |  |
| nextOffset | integer |  |
| offset | integer |  |
| results | Array[Account Policy] | An array of the Policies associated with the Account |
| totalCount | integer | The total number of policies associated with the Account |


### Results Definition

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
          "backupIntervalHours": 12,
          "policyId": "18b4bdd3-cbdf-40c5-86bf-3c36b0a060f5"
        }
      ],
      "totalCount": 2
    }