{{{
  "title": "Get Policy Details By Server",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "false"
}}}

Get policy details by server. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get a list of policies and policy details for all policies associated with a specified server.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/serverPolicyDetails

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/serverPolicyDetails?serverId=VA1BAAPPRDTST01

## Request

### QueryString Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| serverId | string | Unique server name | Yes |
| withStatus | Array[string] | Status of the backup policy. 'ACTIVE','INACTIVE','PROVISIONING','ERROR','DELETED' | No |


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| accountPolicyId | string | Unique ID of an account policy |
| osType | string | 'Linux' or 'Windows' |
| name | string | The name of the Policy |
| clcAccountAlias | string | The account alias that the Policy belongs to |
| accountPolicyStatus | string | The status of the backup Policy. Either 'ACTIVE' or 'INACTIVE' |
| paths | Array[string] | A list of the directories that the Policy includes in each backup |
| backupProvider | string | Not currently used |
| retentionDays | integer | The number of days backup data will be retained |
| backupIntervalHours | integer | The backup frequency of the Policy specified in hours  |
| serverPolicyId | string | Unique server policy identifier |
| serverId | string | Unique server identifier |
| storageRegion | string | Region where backups are stored. "US EAST", "US WEST", "CANADA", "GREAT BRITAIN", "GERMANY", "APAC" |
| serverPolicyStatus | Array[string] | Status of the backup policy. 'ACTIVE','INACTIVE','PROVISIONING','ERROR','DELETED' |
| eligibleForBackup | boolean | Indicates if the account policy or server policy are active/inactive |

### Examples

#### JSON

    {
      [2]
      0:  {
      "accountPolicyId": "5323900d-1288-47c8-9cce-e29790c9afbb"
      "osType": "Windows"
      "name": "TestingPolicy_1/12/16"
      "clcAccountAlias": "BAAP"
      "accountPolicyStatus": "ACTIVE"
      "paths": [2]
      0:  "C:\BackupFolder1"
      1:  "C:\BackupFolder12"
      -
      "backupProvider": null
      "retentionDays": 2
      "backupIntervalHours": 22
      "serverPolicyId": "6d05d351-9cb8-4fed-bca6-064e3034caeb"
      "serverId": "VA1BAAPPRDTST01"
      "storageRegion": "CANADA"
      "serverPolicyStatus": "ACTIVE"
      "eligibleForBackup": true
      }-
      1:  {
      "accountPolicyId": "16965823-5472-49c1-a38a-727dca9cb7a0"
      "osType": "Windows"
      "name": "C Drive"
      "clcAccountAlias": "BAAP"
      "accountPolicyStatus": "ACTIVE"
      "paths": [1]
      0:  "C:\"
      -
      "backupProvider": null
      "retentionDays": 21
      "backupIntervalHours": 2
      "serverPolicyId": "f37088d7-22ba-4704-ba61-25ecd2e8a086"
      "serverId": "VA1BAAPPRDTST01"
      "storageRegion": "US EAST"
      "serverPolicyStatus": "ACTIVE"
      "eligibleForBackup": true
      }
    }
