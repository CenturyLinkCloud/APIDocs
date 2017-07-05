{{{
  "title": "Delete an Intra Data Center Firewall Policy",
  "date": "6-12-2015",
  "author": "Jared Ruckle",
  "attachments": []
}}}

Deletes a firewall policy for a given account in a given data center ("intra data center firewall policy"). Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you need to delete a firewall policy in a given data center for a given account.

  NOTE: This API operation is experimental only, and subject to change with no notice. Please plan accordingly.

## URL

### Structure

    DELETE https://api.ctl.io/v2-experimental/firewallPolicies/{sourceAccountAlias}/{dataCenter}/{firewallPolicy}

### Example

    DELETE https://api.ctl.io/v2-experimental/firewallPolicies/SRC_ALIAS/WA1/1ac853b00e1011e5b9390800200c9a66

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| sourceAccountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the target data center for the new policy. Valid codes can be retrieved from the [Get Data Center List](../Data Centers/get-data-center.md) API operation. | Yes |
| firewallPolicy | string | ID of the firewall policy  | Yes |

## Response

### Entity Definition

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon the successful removal of the firewall policy.
