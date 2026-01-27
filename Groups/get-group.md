{{{
  "title": "Get Group",
  "date": "10-15-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the details for a individual server group and any sub-groups and servers that it contains. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to identify the servers in a particular group, retrieve a group hierarchy, or get links to information (e.g. billing, monitoring, scheduled activities) about a group.

## URL

### Structure

    GET https://api.ctl.io/v2/groups/{accountAlias}/{groupId}

### Example

    GET https://api.ctl.io/v2/groups/ALIAS/2a5c0b9662cf4fc8bf6180f139facdc0

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account. | Yes |
| GroupID | string | ID of the group being queried. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal. | Yes |

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
      "id": "2a5c0b9662cf4fc8bf6180f139facdc0",
      "name": "Web Applications",
      "description": "public facing web apps",
      "locationId": "WA1",
      "type": "default",
      "status": "active",
      "serversCount": 2,
      "groups": [
        {
          "id": "31d13f501459411ba59304f3d47486eb",
          "name": "Training Environment",
          "description": "Temporary servers",
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
              "href": "/v2/groups/acct/31d13f501459411ba59304f3d47486eb",
              "verbs":[
                "GET",
                "PATCH",
                "DELETE"
              ]
            },
            {
              "rel": "parentGroup",
              "href": "/v2/groups/acct/231c3f3fec0e46499290b351199d555f",
              "id": "231c3f3fec0e46499290b351199d555f"
            },
            {
              "rel": "defaults",
              "href": "/v2/groups/acct/31d13f501459411ba59304f3d47486eb/defaults",
              "verbs":[
                "GET",
                "POST"
              ]
            },  
            {
              "rel": "billing",
              "href": "/v2/groups/acct/31d13f501459411ba59304f3d47486eb/billing"
            },
            {
              "rel": "archiveGroupAction",
              "href": "/v2/groups/acct/31d13f501459411ba59304f3d47486eb/archive"
            },
            {
              "rel": "statistics",
              "href": "/v2/groups/acct/31d13f501459411ba59304f3d47486eb/statistics"
            },
            {
              "rel":"upcomingScheduledActivities",
              "href":"/v2/groups/acct/8a03fcae8dd65411b05f00505682315a/upcomingScheduledActivities"
            },
            {
              "rel":"horizontalAutoscalePolicyMapping",
              "href":"/v2/groups/acct/31d13f501459411ba59304f3d47486eb/horizontalAutoscalePolicy",
              "verbs":[
                "GET",
                "PUT",
                "DELETE"
              ]
            },
            {
              "rel": "scheduledActivities",
              "href": "/v2/groups/acct/31d13f501459411ba59304f3d47486eb/scheduledActivities"
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
          "href": "/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0"
        },
        {
          "rel": "parentGroup",
          "href": "/v2/groups/acct/540494152d0c4a9ab61869562b4c1471",
          "id": "540494152d0c4a9ab61869562b4c1471"
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
          "rel": "scheduledActivities",
          "href": "/v2/groups/acct/2a5c0b9662cf4fc8bf6180f139facdc0/scheduledActivities"
        },
        {
          "rel": "server",
          "href": "/v2/servers/acct/wa1acctpre7101",
          "id": "WA1ACCTPRE7101"
        },
        {
          "rel": "server",
          "href": "/v2/servers/btdi/wa1acctpre7202",
          "id": "WA1ACCTPRE7202"
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
