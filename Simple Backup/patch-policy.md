{{{
  "title": "Patch Policy",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "false"
}}}

Updates specific values of a server policy. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Because of the business rules that apply to this product, there are limited scenarios when this operation is allowed.  Specifically, you may use this API operation when you want to change the status of a server policy from 'ERROR', 'PENDING_INSTALL', or 'PROVISIONING' to 'INACTIVE'.  Other attempts to modify the server policy will result in errors.

## URL

### Structure

    PATCH https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}/serverPolicies/{serverPolicyId}

### Example

    PATCH https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/c8cbf556-9ea1-4759-8d4e-c788198af26c/serverPolicies/ce0eefe2-25b8-4320-ba68-eeda76aef2dc

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountPolicyId | string | Unique ID of an account policy | Yes |
| serverPolicyId | string | Unique Id of the Server Policy | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| op | string | The patch operation to perform: 'add', 'remove', 'replace' | Yes |
| path | string | The only change allowed currently is to the status.  Valid transitions are: ERROR to INACTIVE, PENDING_INSTALL to INACTIVE, and PROVISIONING to INACTIVE | Yes |
| value | string | The new value to set path to. | Yes |

### Examples

#### JSON

    {
      "op": "replace",
      "path": "/status",
      "value": "INACTIVE"
    }



## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| serverPolicyId | string | Unique Id of the Server Policy |
| accountPolicyId | string | Unique Id of the Account Policy |
| serverId | string | Unique server name |
| storageRegion | string | Region where backups are stored |
| clcAccountAlias | string | The account alias that the Policy belongs to |
| status | string | The status of the backup Policy. 'ACTIVE', 'INACTIVE', 'PROVISIONING', 'ERROR', 'DELETED' |
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
