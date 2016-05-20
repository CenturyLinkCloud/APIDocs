{{{
  "title": "Get Cross Data Center Firewall Policy List",
  "date": "5-24-2016",
  "author": "Anthony Hakim",
  "attachments": [],
  "contentIsHTML": false
}}}

Gets the list of firewall policies associated with a given account, between networks in different data centers ("cross data center firewall policies"). Users can optionally filter results by requesting policies associated with a second "destination" account. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](https://www.ctl.io/api-docs/v2/#authentication-login) for information on acquiring this token.

### When to Use It

Use this API operation when you need the list of available firewall policies between networks in different data centers.

  NOTE: This API operation is experimental only, and subject to change without notice. Please plan accordingly.

## URL

### Structure

    GET https://api.ctl.io/v2-experimental/crossDcFirewallPolicies/{sourceAccountAlias}/{dataCenter}?destinationAccountId=<other account id>

### Example

    GET https://api.ctl.io/v2-experimental/crossDcFirewallPolicies/SRC_ALIAS/VA1?destinationAccountAlias=DEST_ALIAS

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| sourceAccountAlias | string | Short code for a particular account | Yes |
| dataCenter | string | Short string representing the target data center for the new policy. Valid codes can be retrieved from the [Get Data Center List](https://www.ctl.io/api-docs/v2/#data-centers-get-data-center) API operation. | Yes |
| destinationAccountAlias | string | Short string for another account | No |

## Response

### Example

#### JSON
```json
[
    {
        "id": "92167034-4d78-1378-a8df-6159c00bddea",
        "status": "active",
        "enabled": true,
        "sourceCidr": "10.2.2.0/24",
        "sourceAccount": "src",
        "sourceLocation": "va1",
        "destinationCidr": "10.1.1.0/24",
        "destinationAccount": "dest",
        "destinationLocation": "uc1",
        "links": [
            {
                "rel": "self",
                "href": "/v2-experimental/crossDcFirewallPolicies/src/va1/92167034-4d78-1378-a8df-6159c00bddea",
                "verbs": [
                    "GET",
                    "PUT",
                    "DELETE"
                ]
            }
        ]
    }
]
```
