{{{
  "title": "Create Group",
  "date": "02-27-2015",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Creates a new group. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to create a new group.

## URL

### Structure

    POST https://api.ctl.io/v2/groups/{accountAlias}

### Example

    POST https://api.ctl.io/v2/groups/ALIAS/

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| name | string | Name of the group to create. | Yes |
| description | string | User-defined description of this group | No |
| parentGroupId | string | ID of the parent group. Retrieved from query to parent group, or by looking at the URL on the UI pages in the Control Portal. | Yes |
| customFields | complex | Collection of custom field ID-value pairs to set for the server. | No |

### CustomFields Definition

| Name | Type | Description |
| --- | --- |--- |
| id | string | ID of the custom field to set. Available custom field IDs can be retrieved from the [Get Custom Fields](../Custom Fields/get-custom-fields.md) API operation. |
| value | string | Value to set the custom field to for this server. |

### Examples

#### JSON

    {
      "name": "New Group",
      "description": "A new group.",
      "parentGroupId": "2a5c0b9662cf4fc8bf6180f139facdc0",
      "customFields": [
        {
          "id": "58f83af6123846769ee6cb091ce3561e",
          "value": "1100003"
        }
      ]
    }

## Response

### Group Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | ID of the group being queried |
| name | string | User-defined name of the group |
| description | string | User-defined description of this group |
| locationId | string | Data center location identifier |
| type | string | Group type which could include system types like "archive" |
| status | string | Describes if group is online or not |
| serversCount | integer | Number of servers this group contains |
| groups | array | Refers to this same entity type for each sub-group |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this group |
| changeInfo | complex | Describes "created" and "modified" details |
| customFields | complex | Details about any custom fields and their values |

### ChangeInfo Definition

| Name | Type | Description |
| --- | --- | --- |
| createdDate | dateTime | Date/time that the group was created |
| createdBy | string | Who created the group |
| modifiedDate | dateTime | Date/time that the group was last updated |
| modifiedBy | string | Who modified the group last |

### CustomFields Definition

| Name | Type | Description |
| --- | --- | --- |
| id | string | Unique ID of the custom field |
| name | string | Friendly name of the custom field |
| value | string | Underlying value of the field |
| displayValue | string | Shown value of the field |

### Examples

#### JSON

    {
      "id": "56b789a2a72f43a98ae2227061e8f8f8",
      "name": "New Group",
      "description": "A new group.",
      "locationId": "WA1",
      "type": "default",
      "status": "active",
      "groups": [
        {
          "id": "2a5c0b9662cf4fc8bf6180f139facdc0",
          "name": "Parent Group Name",
          "description": "The parent group.",
          "locationId": "WA1",
          "type": "default",
          "status": "active",
          "serversCount": 0,
          "groups": [],
          "links": [
            {
              "rel":"createGroup",
              "href":"/v2/groups/acct",
              "verbs":[
                "POST"
              ]
            },
            {
              "rel":"createServer",
              "href":"/v2/servers/acct",
              "verbs":[
                "POST"
              ]
            },
            {
              "rel": "self",
              "href": "/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0",
              "verbs":[
                "GET",
                "PATCH",
                "DELETE"
              ]
            },
            {
              "rel": "parentGroup",
              "href": "/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0",
              "id": "2a5c0b9662cf4fc8bf6180f139facdc0"
            },
            {
              "rel": "defaults",
              "href": "/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0/defaults",
              "verbs":[
                "GET",
                "POST"
              ]
            },  
            {
              "rel": "billing",
              "href": "/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0/billing"
            },
            {
              "rel": "archiveGroupAction",
              "href": "/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0/archive"
            },
            {
              "rel": "statistics",
              "href": "/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0/statistics"
            },
            {
              "rel":"upcomingScheduledActivities",
              "href":"/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0/upcomingScheduledActivities"
            },
            {
              "rel":"horizontalAutoscalePolicyMapping",
              "href":"/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0/horizontalAutoscalePolicy",
              "verbs":[
                "GET",
                "PUT",
                "DELETE"
              ]
            },
            {
              "rel": "scheduledActivities",
              "href": "/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0/scheduledActivities"
              "verbs":[
                "GET",
                "POST"
              ]
            }
          ]
        }
      ],
      "links":[
        {
          "rel": "self",
          "href": "/v2/groups/acct/56b789a2a72f43a98ae2227061e8f8f8"
        },
        {
          "rel": "parentGroup",
          "href": "/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0",
          "id": "2a5c0b9662cf4fc8bf6180f139facdc0"
        },
        {
          "rel": "billing",
          "href": "/v2/groups/acct/56b789a2a72f43a98ae2227061e8f8f8/billing"
        },
        {
          "rel": "archiveGroupAction",
          "href": "/v2/groups/acct/56b789a2a72f43a98ae2227061e8f8f8/archive"
        },
        {
          "rel": "statistics",
          "href": "/v2/groups/acct/56b789a2a72f43a98ae2227061e8f8f8/statistics"
        },
        {
          "rel": "scheduledActivities",
          "href": "/v2/groups/acct/56b789a2a72f43a98ae2227061e8f8f8/scheduledActivities"
        }
      ],
      "changeInfo": {
        "createdDate": "2012-12-17T01:17:17Z",
        "createdBy": "user@domain.com",
        "modifiedDate": "2014-05-16T23:49:25Z",
        "modifiedBy": "user@domain.com"
      },
      "customFields": [
        {
          "id": "22f002123e3b46d9a8b38ecd4c6df7f9",
          "name": "Cost Center",
          "value": "IT-DEV",
          "displayValue": "IT-DEV"
        },
        {
          "id": "58f83af6123846769ee6cb091ce3561e",
          "name": "CMDB ID",
          "value": "1100003",
          "displayValue": "1100003"
        }
      ]
    }
