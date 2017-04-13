{{{
  "title": "Get Server Policy",
  "date": "04-01-2016",
  "author": "Justin Withington",
  "attachments": [],
  "sticky": "false"
}}}

Get details of a specific server policy associated to an account policy. A server policy is unique record that ties a backup (account) policy to a specific server and storage region. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get details for a specific server policy. Use the getServerPolicies API to obtain details for all server policies associated with an account policy.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}/serverPolicies/{serverPolicyId}

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/c8cbf556-9ea1-4759-8d4e-c788198af26c/serverPolicies/ce0eefe2-25b8-4320-ba68-eeda76aef2dc

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountPolicyId | string | Unique ID of an account policy | Yes |
| serverPolicyId | string | Unique Id of the Server Policy | Yes |


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| serverPolicyId | string | Unique Id of the Server Policy |
| accountPolicyId | string | Unique Id of the Account Policy |
| serverId | string | Unique server name |
| storageRegion | string | Region where backups are stored |
| clcAccountAlias | string | The account alias that the Policy belongs to |
| status | string | The status of the backup Policy. 'ACTIVE', 'INACTIVE', 'PROVISIONING', 'ERROR', 'DELETED', 'PENDING_INSTALL' |
| expirationDate | integer | Date all data retention will elapse; unsubscribedDate+retentionDays |
| unsubscribedDate | integer | Date policy was inactivated |
| storageAccountId | string | Not currently used |


### Examples

#### JSON

    {
      "serverPolicyId": "ce0eefe2-25b8-4320-ba68-eeda76aef2dc"
      "accountPolicyId": "c8cbf556-9ea1-4759-8d4e-c788198af26c"
      "serverId": "IL1BAAPDEMO101"
      "storageRegion": "US WEST"
      "clcAccountAlias": "BAAP"
      "status": "ACTIVE"
      "expirationDate": 0
      "unsubscribedDate": 0
      "storageAccountId": null
    }
