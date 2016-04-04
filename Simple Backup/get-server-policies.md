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

    GET https://api-va1.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}/serverPolicies

### Example

    GET https://api-va1.backup.ctl.io/clc-backup-api/api/accountPolicies/7796a750-db6a-4d6d-a9c0-93f729e9977e/serverPolicies

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountPolicyId | string | Unique ID of an existing account policy | Yes |
| limit | integer | | No |
| offset | string | | No |
| withStatus | string |  | No |
| sortBy | string |  | No |
| ascendingSort | boolean | Sort the sortBy field in ascending order | No |


## Response

### Server Policies Definition

| Name | Type | Description |
| --- | --- | --- |
| limit | integer |  |
| offset | integer |  |
| nextOffset | integer |  |
| results | Array[Server Policy] | An array of the Server Policies associated with the Account Policy |
| totalCount | integer | The total number of Server Policies associated with the Account Policy |


### Results Definition

| Name | Type | Description |
| --- | --- | --- |
| serverPolicyId | string | |
| accountPolicyId | string | |
| serverId | string | |
| storageRegion | string | |
| clcAccountAlias | string | |
| status | string | |
| expirationDate | integer | |
| unsubscribedDate | integer | |
| storageAccountId | string | |



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
