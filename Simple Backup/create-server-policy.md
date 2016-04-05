{{{
  "title": "Get Policies",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "true"
}}}

Create a Server Policy under an Account Policy. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new Server Policy.

## URL

### Structure

    PUT https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}/serverPolicies

### Example

    PUT https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/5fde14a2-fa9d-4376-9f01-59429d02a959/serverPolicies

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountPolicyId | string | The unique Id of an account policy | Yes |


## Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| clcAccountAlias | string | The account alias that the Policy belongs to | Yes |
| serverId | string | Name of the server to apply the policy to | Yes|
| storageRegion | string | "US EAST", "US WEST", "CANADA", "GREAT BRITAIN", "GERMANY", "APAC" | Yes|


### Examples

#### JSON

    {
      "clcAccountAlias": "BAAD",
      "serverId": "VA1BAADTEST01",
      "storageRegion": "USEAST",
    }


## Response

### Server Policy Definition

| Name | Type | Description |
| --- | --- | --- |
| serverPolicyId | string | ID of the server policy being created |
| accountPolicyId | string | |
| serverId | string | |
| storageRegion | string | |
| clcAccountAlias | string | |
| status | string | |
| expirationDate | integer | |
| unsubscribedDate | integer | |
| storageAccountId | null | |


### Examples

#### JSON

    {
    "serverPolicyId": "085384ce-200e-4205-8a13-ae1d0bdc71cd"
    "accountPolicyId": "5fde14a2-fa9d-4376-9f01-59429d02a959"
    "serverId": "VA1BAADTEST01"
    "storageRegion": "US EAST"
    "clcAccountAlias": "BAAD"
    "status": "PROVISIONING"
    "expirationDate": 0
    "unsubscribedDate": 0
    "storageAccountId": null
    }
