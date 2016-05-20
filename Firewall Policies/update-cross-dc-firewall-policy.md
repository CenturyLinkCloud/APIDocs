{{{
  "title": "Update Cross Data Center Firewall Policy",
  "date": "5-24-2016",
  "author": "Anthony Hakim",
  "attachments": [],
  "contentIsHTML": false
}}}

Updates a given firewall policy associated with a given account, between networks in different data centers ("cross data center firewall policy"). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you need to update a firewall policy between networks in different data centers.

  NOTE: This API operation is experimental only, and subject to change without notice. Please plan accordingly.

## URL

### Structure

    PUT https://api.ctl.io/v2-experimental/crossDcFirewallPolicies/{sourceAccountAlias}/{dataCenter}/{policyId}?enabled=true/false

### Example

    PUT https://api.ctl.io/v2-experimental/crossDcFirewallPolicies/SRC_ALIAS/VA1/92167034-4d78-1378-a8df-6159c00bddea?enabled=false

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| sourceAccountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the data center associated with the policy of interest. Valid codes can be retrieved from the [Get Data Center List](https://www.ctl.io/api-docs/v2/#data-centers-get-data-center) API operation. | Yes |
| enabled | string | true or false | Yes |

## Response

There is no response upon the successful update of the firewall policy.
