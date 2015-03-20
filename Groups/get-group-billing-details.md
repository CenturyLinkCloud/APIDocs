{{{
  "title": "Get Group Billing Details",
  "date": "10-13-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the current and estimated charges for each server in a designated group hierarchy. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to find out the charges associated with a specific group.

## URL

### Structure

    GET https://api.ctl.io/v2/groups/{accountAlias}/{groupId}/billing

### Example

    GET https://api.ctl.io/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0/billing

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| GroupID | string | ID of the group being queried. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal | Yes |

## Response

### Group Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| date | datetime | Date that this billing information applies to |
| groups | array | List of groups (with the first being the queried group) in the requested hierarchy. Group ID listed before each group entity description |

### Groups Definition

| Name | Type | Description |
| --- | --- | --- |
| name | string | User-defined name of the group |
| servers | array | Collection of servers in this group, each with billing information. Server ID listed before each entity description |

### Servers Definition

| Name | Type | Description |
| --- | --- | --- |
| templateCost | float | Cost of templates stored in the group |
| archiveCost | float | Cost of archived servers in this group |
| monthlyEstimate | float | Projected charges for the servers given current usage |
| monthToDate | float | Charges up until the requested time |
| currentHour | float | Charges for the most recent hour |

### Examples

#### JSON


    {
      "date": "2014-04-07T21:33:51.9743015Z",
      "groups": {
        "8c95fbaf74b7497fb671235aa318b44c": {
          "name": "Web Applications",
          "servers": {
            "wa1acctserv7101": {
              "templateCost": 0.0,
              "archiveCost": 0.0,
              "monthlyEstimate": 77.76,
              "monthToDate": 17.93,
              "currentHour": 0.108
            },
            "wa1acctserv7202": {
              "templateCost": 0.0,
              "archiveCost": 0.0,
              "monthlyEstimate": 156.96,
              "monthToDate": 36.19,
              "currentHour": 0.218
            }
          }
        },
        "4bca7bf6ead14cd59053e1eb1cd2d01f": {
          "name": "Training Environment",
          "servers": {}
        }
      }
    }
