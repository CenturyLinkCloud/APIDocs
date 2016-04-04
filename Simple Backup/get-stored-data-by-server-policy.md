{{{
  "title": "Get Policies",
  "date": "04-01-2016",
  "author": "Ryan Brockman",
  "attachments": [],
  "sticky": "true"
}}}

Gets the amount of stored data for a server policy on a specified date. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to determine the amount of backed up data in storage for a server on a specific day.

## URL

### Structure

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/{accountPolicyId}/serverPolicies/{serverPolicyId}/storedData

### Example

    GET https://api.backup.ctl.io/clc-backup-api/api/accountPolicies/c8cbf556-9ea1-4759-8d4e-c788198af26c/serverPolicies/ce0eefe2-25b8-4320-ba68-eeda76aef2dc/storedData?searchDate=2016-03-29


## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| accountPolicyId | string | Unique account policy identifier | Yes |
| serverPolicyId | string | Unique server policy identifier | Yes |
| searchDate | string | Valid date format is 'YYYY-MM-DD' | Yes |

## Response

### Response Definition

| Name | Type | Description |
| --- | --- | --- |
| gigabytesStored | string | Amount of stored backup data in gigabytes |
| bytesStored | string | Amount of stored backup data in bytes |

### Examples

#### JSON

    {
      "gigabytesStored": "0.541"
      "bytesStored": "581560320"
    }
