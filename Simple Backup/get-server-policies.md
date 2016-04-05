{{{
  "title": "Get Policies",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "true"
}}}

Gets a list of Server Policies associated to an Account Policy. A server policy is unique record that ties a backup (account) policy to a specific server and storage region. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to get a list of all Server Policies attached to an Account Policy.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}/serverPolicies

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/5fde14a2-fa9d-4376-9f01-59429d02a959/serverPolicies

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountPolicyId | string | Unique ID of an account policy | Yes |
| limit | integer | Return up to this many results | No |
| offset | string | Return results starting from this position in the list | No |
| withStatus | string | Filter results for either 'ACTIVE' or 'INACTIVE' Policies | No |
| sortBy | string | Sort the results by the specified field | No |
| ascendingSort | boolean | Sort the sortBy field in ascending order | No |


## Response

### Server Policies Definition

| Name | Type | Description |
| --- | --- | --- |
| limit | integer | The maximum number of results requested |
| offset | integer | The starting position in the list of results |
| nextOffset | integer | The next position in the list of results for a subsequent call |
| results | Array[Server Policy] | An array of the Server Policies associated with the Account Policy |
| totalCount | integer | The total number of Server Policies associated with the Account Policy |


### Results Definition

| Name | Type | Description |
| --- | --- | --- |
| serverPolicyId | string | The next position in the list of results for a subsequent call |
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
      "limit": 1000
      "offset": 0
      "nextOffset": 0
      "results": [1]
          0:  {
              "serverPolicyId": "7796a750-db6a-4d6d-a9c0-93f729e9977e"
              "accountPolicyId": "5fde14a2-fa9d-4376-9f01-59429d02a959"
              "serverId": "VA1BAADTEST01"
              "storageRegion": "US EAST"
              "clcAccountAlias": "BAAD"
              "status": "ACTIVE"
              "expirationDate": 0
              "unsubscribedDate": 0
              "storageAccountId": "f5c2c756-94b6-4b74-92e9-60f648caed15"
              }
      "totalCount": 1
      }
