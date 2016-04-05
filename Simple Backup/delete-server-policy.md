{{{
  "title": "Delete Server Policy",
  "date": "04-01-2016",
  "author": "John Gerger",
  "attachments": [],
  "sticky": "false"
}}}

Delete a Server Policy under an Account Policy. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete an existing Server Policy.

## URL

### Structure

    DELETE https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}/serverPolicies/{serverPolicyId}

### Example

    DELETE https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/5fde14a2-fa9d-4376-9f01-59429d02a959/serverPolicies/085384ce-200e-4205-8a13-ae1d0bdc71cd

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| serverPolicyId | string | Unique Id of the Server Policy | Yes |
| accountPolicyId | string | Unique Id of the Account Policy | Yes |


## Response

### Server Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| HTTP status code | string | HTTP status code |


### Examples

#### RESPONSE

204: No Content
