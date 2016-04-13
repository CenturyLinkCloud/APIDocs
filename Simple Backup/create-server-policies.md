{{{
  "title": "Create Server Policies",
  "date": "04-12-2016",
  "author": "Justin Withington",
  "attachments": [],
  "sticky": "false"
}}}

Create multiple Server Policies under an Account Policy. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create multiple Server Policies.

## URL

### Structure

    POST https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}/serverPolicies

### Example

    POST https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/193fccfc-c144-4052-98da-145eed825e0a/serverPolicies

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountPolicyId | string | The unique Id of an account policy | Yes |


## Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| clcAccountAlias | string | The account alias that the Policy belongs to | Yes |
| serverId | string | Unique server name | Yes|
| storageRegion | string | Region where backups are stored, can be "US EAST", "US WEST", "CANADA", "GREAT BRITAIN", "GERMANY", "APAC" | Yes|


### Examples

#### JSON

    {
      "serverId": "UC1BAADTEST01",
      "storageRegion": "US WEST"
     },{
      "serverId": "IL1BAADTEST01",
      "storageRegion": "US WEST"
    }


## Response

### Response List Definition

| Name | Type | Description |
| --- | --- | --- |
| status | string | Aggregate status for entire server policy creation request. 'SUCCESS', 'PARTIAL', 'FAILED' |
| success | boolean | Indicates if server policy creation was successful |
| error | string | Provides details for server policy creation failure related to system or infrastructure |
| validationMessages | string | Provides details for server policy creation failure related to parameter restrictions |

### Server Policy Definition

| Name | Type | Description |
| --- | --- | --- |
| serverPolicyId | string | Unique Id of the Server Policy |
| accountPolicyId | string | Unique Id of the Account Policy |
| serverId | string | Unique server name |
| storageRegion | string | Region where backups are stored |
| clcAccountAlias | string | The account alias that the Policy belongs to |
| status | string | The status of the backup Policy. 'ACTIVE', 'INACTIVE', 'PROVISIONING', 'ERROR', 'DELETED' |
| expirationDate | integer | Date all data retention will elapse; unsubscribedDate+retentionDays |
| unsubscribedDate | integer | Date policy was inactivated|
| storageAccountId | null | Not currently used |


### Examples

#### JSON

    {
     "status": "PARTIAL",
     "createServerPolicyResponseList": [
      {
      "success": false,
      "error": "Failed to get server information for serverId=UC1BAADTEST01",
      "validationMessages": null,
      "serverPolicy": {
        "serverPolicyId": null,
        "accountPolicyId": null,
        "serverId": "UC1BAADTEST01",
        "storageRegion": "US WEST",
        "clcAccountAlias": "BAAD",
        "status": null,
        "expirationDate": 0,
        "unsubscribedDate": 0,
        "storageAccountId": null
        }
      },
      {
      "success": true,
      "error": null,
      "validationMessages": null,
      "serverPolicy": {
        "serverPolicyId": "80448207-332c-4f95-b82b-ac1fcb87b2c6",
        "accountPolicyId": "193fccfc-c144-4052-98da-145eed825e0a",
        "serverId": "IL1BAADTEST01",
        "storageRegion": "US WEST",
        "clcAccountAlias": "BAAD",
        "status": "PROVISIONING",
        "expirationDate": 0,
        "unsubscribedDate": 0,
        "storageAccountId": null
        }
      }
     ]
    }
