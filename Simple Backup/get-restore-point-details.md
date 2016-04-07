{{{
  "title": "Get Restore Point Details",
  "date": "04-01-2016",
  "author": "Justin Withington",
  "attachments": [],
  "sticky": "false"
}}}

Gets a list of restore point details. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to obtain restore point details for a specific serverPolicyId.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}/serverPolicies/{serverPolicyId}/restorePointDetails

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}/serverPolicies/ce0eefe2-25b8-4320-ba68-eeda76aef2dc/restorePointDetails?backupFinishedStartDate=2016-01-01&backupFinishedEndDate=2016-04-01

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| serverPolicyId | string | Unique Id of the Server Policy | Yes |
| accountPolicyId | string | Unique Id of the Account Policy | Yes |

### QueryString Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| limit | integer | Limit the number of records returned | No
| offset | integer |  | No
| inRetentionOnly | boolean |  | No
| backupFinishedStartDate | string | Valid date format is 'YYYY-MM-DD' | Yes
| backupFinishedEndDate | string | Valid date format is 'YYYY-MM-DD' | Yes
| sortBy | string | Sort results by: [policyId, retentionDay, backupStartedDate, backupFinishedDate, retentionExpiredDate, backupStatus, filesTransferredToStorage, bytesTransferredToStorage, filesFailedTransferToStorage, bytesFailedToTransfer, unchangedFilesNotTransferred, unchangedBytesNotTransferred, filesRemovedFromDisk, bytesRemovedFromDisk] | No
| ascendingSort | boolean |  | No
| serverPolicyId | string | Unique server policy identifier | Yes


## Response

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| restorePointId | string | Unique restore point identifier |
| policyId | string | Unique policy identifier |
| retentionDays | integer | Days of retention applied to the restore point |
| backupFinishedDate | string | Timestamp of backup completion |
| retentionExpiredDate | string | Timestamp or retention expiration |
| restorePointCreationStatus | string | 'SUCCESS', 'PARTIAL_SUCCESS', 'FAILED', or 'CANCELLED'  |
| filesTransferredToStorage | integer | Number of backup files transferred to storage |
| bytesTransferredToStorage | integer | Total bytes of backup data sent to storage |
| filesFailedTransferToStorage | integer | Number of backup files that failed transfer to storage |
| bytesFailedToTransfer | integer | Total bytes of backup data that failed transfer to storage |
| unchangedFilesNotTransferred | integer | Number of unchanged files not requiring retransfer to storage |
| unchangedBytesInStorage | integer | Total bytes of unchanged data not requiring retransfer to storage |
| filesRemovedFromDisk | integer | Number of files removed from local disk |
| bytesInStorageForItemsRemoved | integer | Total bytes of data removed from local disk |
| numberOfProtectedFiles | integer | Number of files currently in storage for the restore point |
| backupStartedDate | string | Timestamp of backup start |

### Examples

#### JSON

    {
      "limit": 100
      "offset": 0
      "nextOffset": 0
      "results": [2]
        0:  {
            "restorePointId": "ce0eefe2-25b8-4320-ba68-eeda76aef2dc20160401225505"
            "policyId": "ce0eefe2-25b8-4320-ba68-eeda76aef2dc"
            "retentionDays": 5
            "backupFinishedDate": "2016-04-01T22:55:10.849Z"
            "retentionExpiredDate": "2016-04-07T22:55:05.277Z"
            "restorePointCreationStatus": "SUCCESS"
            "filesTransferredToStorage": 0
            "bytesTransferredToStorage": 0
            "filesFailedTransferToStorage": 0
            "bytesFailedToTransfer": 0
            "unchangedFilesNotTransferred": 3
            "unchangedBytesInStorage": 388403200
            "filesRemovedFromDisk": 0
            "bytesInStorageForItemsRemoved": 0
            "numberOfProtectedFiles": 3
            "backupStartedDate": "2016-04-01T22:55:05.277Z"
      }
      -1:   {
            "restorePointId": "ce0eefe2-25b8-4320-ba68-eeda76aef2dc20160401214505"
            "policyId": "ce0eefe2-25b8-4320-ba68-eeda76aef2dc"
            "retentionDays": 5
            "backupFinishedDate": "2016-04-01T21:45:10.802Z"
            "retentionExpiredDate": "2016-04-07T21:45:05.261Z"
            "restorePointCreationStatus": "SUCCESS"
            "filesTransferredToStorage": 0
            "bytesTransferredToStorage": 0
            "filesFailedTransferToStorage": 0
            "bytesFailedToTransfer": 0
            "unchangedFilesNotTransferred": 3
            "unchangedBytesInStorage": 388403200
            "filesRemovedFromDisk": 0
            "bytesInStorageForItemsRemoved": 0
            "numberOfProtectedFiles": 3
            "backupStartedDate": "2016-04-01T21:45:05.261Z"
      }
      "totalCount": 2
    }
