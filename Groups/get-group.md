{{{
  "title": "Get Group",
  "date": "10-15-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the details for a individual server group and any sub-groups and servers that it contains. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to identify the servers in a particular group, retrieve a group hierarchy, or get links to information (e.g. billing, monitoring, scheduled activities) about a group.

## URL

### Structure

    GET https://api.tier3.com/v2/groups/{accountAlias}/{groupId}

### Example

    GET https://api.tier3.com/v2/groups/ALIAS/wa1-0001

## Request

### URI Parameters

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Req.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AccountAlias</td>
      <td>string</td>
      <td>Short code for a particular account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GroupID</td>
      <td>string</td>
      <td>ID of the group being queried. Retrieved from query to parent group, or by looking at the URL on the new UI pages in the Control Portal.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

## Response

### Group Entity Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>ID of the group being queried</td>
    </tr>
    <tr>
      <td>name</td>
      <td>string</td>
      <td>User-defined name of the group</td>
    </tr>
    <tr>
      <td>description</td>
      <td>string</td>
      <td>User-defined description of this group</td>
    </tr>
    <tr>
      <td>locationId</td>
      <td>string</td>
      <td>Data center location identifier</td>
    </tr>
    <tr>
      <td>type</td>
      <td>string</td>
      <td>Group type which could include system types like "archive"</td>
    </tr>
    <tr>
      <td>status</td>
      <td>string</td>
      <td>Describes if group is online or not</td>
    </tr>
    <tr>
      <td>serversCount</td>
      <td>integer</td>
      <td>Number of servers this group contains</td>
    </tr>
    <tr>
      <td>groups</td>
      <td>array</td>
      <td>Refers to this same entity type for each sub-group</td>
    </tr>
    <tr>
      <td>links</td>
      <td>array</td>
      <td>Collection of entity links that point to resources related to this group</td>
    </tr>
    <tr>
      <td>changeInfo</td>
      <td>complex</td>
      <td>Describes "created" and "modified" details</td>
    </tr>
    <tr>
      <td>customFields</td>
      <td>complex</td>
      <td>Details about any custom fields and their values</td>
    </tr>
  </tbody>
</table>

### Create Group Link

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>createGroup</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/groups/[ALIAS]</td>
      <td>Address of the resource itself</td>
    </tr>
    <tr>
      <td>verbs</td>
      <td>array</td>
      <td>POST</td>
      <td>Valid HTTP verbs that can act on this resource</td>
    </tr>
  </tbody>
</table>

### Create Server Link

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>createServer</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/servers/[ALIAS]</td>
      <td>Address of the resource itself</td>
    </tr>
    <tr>
      <td>verbs</td>
      <td>array</td>
      <td>POST</td>
      <td>Valid HTTP verbs that can act on this resource</td>
    </tr>
  </tbody>
</table>


### Self Link Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>self</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/groups/[ALIAS]/[GROUPID]</td>
      <td>Address of the resource itself</td>
    </tr>
    <tr>
      <td>verbs</td>
      <td>array</td>
      <td>GET | PATCH | DELETE</td>
      <td>Valid HTTP verbs that can act on this resource</td>
    </tr>
  </tbody>
</table>

### Parent Group Link Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>parentGroup</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/groups/[ALIAS]/[GROUPID]</td>
      <td>Address of the parent group</td>
      </tr>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>[GROUPID]</td>
      <td>Unique ID of the parent group</td>
    </tr>
  </tbody>
</table>

## Defaults Link

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>defaults</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/groups/[ALIAS]/[GROUPID]/defaults</td>
      <td>Address of the resource itself</td>
    </tr>
    <tr>
      <td>verbs</td>
      <td>array</td>
      <td>GET | POST</td>
      <td>Valid HTTP verbs that can act on this resource</td>
    </tr>
  </tbody>
</table>

### Billing Link Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>billing</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/groups/[ALIAS]/[GROUPID]/billing</td>
      <td>Address of the billing information for the group</td>
    </tr>
  </tbody>
</table>

### Archive Link Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>archiveGroupAction</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/groups/[ALIAS]/[GROUPID]/archive</td>
      <td>Address of the archive details for this group</td>
    </tr>
  </tbody>
</table>

### Statistics Link Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>statistics</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/groups/[ALIAS]/[GROUPID]/statistics</td>
      <td>Address of usage statistics for this group</td>
    </tr>
  </tbody>
</table>

### Upcoming Scheduled Activities Link Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>upcomingScheduledActivities</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/groups/[ALIAS]/[GROUPID]/upcomingScheduledActivities</td>
      <td>Address of the resource itself</td>
    </tr>
  </tbody>
</table>

### Scheduled Activities Link Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>scheduledActivities</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/groups/[ALIAS]/[GROUPID]/scheduledActivities</td>
      <td>Address of the scheduled activities (e.g. restarts, pause) for this group</td>
    </tr>
    <tr>
      <td>verbs</td>
      <td>array</td>
      <td>GET | POST</td>
      <td>Valid HTTP verbs that can act on this resource</td>
    </tr>
  </tbody>
</table>

### Server Link

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Value</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>rel</td>
      <td>string</td>
      <td>server</td>
      <td>The link type</td>
    </tr>
    <tr>
      <td>href</td>
      <td>string</td>
      <td>/v2/servers/[ALIAS]/[SERVERID]</td>
      <td>Address of the server in this group</td>
    </tr>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>[SERVERID]</td>
      <td>ID of the server in this group</td>
    </tr>
  </tbody>
</table>

### ChangeInfo Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>createdDate</td>
      <td>dateTime</td>
      <td>Date/time that the group was created</td>
    </tr>
    <tr>
      <td>createdBy</td>
      <td>string</td>
      <td>Who created the group</td>
    </tr>
    <tr>
      <td>modifiedDate</td>
      <td>dateTime</td>
      <td>Date/time that the group was last updated</td>
    </tr>
    <tr>
      <td>modifiedBy</td>
      <td>string</td>
      <td>Who modified the group last</td>
    </tr>
  </tbody>
</table>

### CustomFields Definition

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>id</td>
      <td>string</td>
      <td>Unique ID of the custom field</td>
    </tr>
    <tr>
      <td>name</td>
      <td>string</td>
      <td>Friendly name of the custom field</td>
    </tr>
    <tr>
      <td>value</td>
      <td>string</td>
      <td>Underlying value of the field</td>
    </tr>
    <tr>
      <td>displayValue</td>
      <td>string</td>
      <td>Shown value of the field</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
      "id": "wa1-0001",
      "name": "Web Applications",
      "description": "public facing web apps",
      "locationId": "WA1",
      "type": "default",
      "status": "active",
      "serversCount": 2,
      "groups": [
        {
          "id": "wa1-0002",
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
              "href": "/v2/groups/acct/wa1-0002",
              "verbs":[
                "GET",
                "PATCH",
                "DELETE"
              ]
            },
            {
              "rel": "parentGroup",
              "href": "/v2/groups/acct/wa1-0002",
              "id": "wa1-0002"
            },
            {
              "rel": "defaults",
              "href": "/v2/groups/acct/wa1-0002/defaults",
              "verbs":[
                "GET",
                "POST"
              ]
            },  
            {
              "rel": "billing",
              "href": "/v2/groups/acct/wa1-0002/billing"
            },
            {
              "rel": "archiveGroupAction",
              "href": "/v2/groups/acct/wa1-0002/archive"
            },
            {
              "rel": "statistics",
              "href": "/v2/groups/acct/wa1-0002/statistics"
            },
            {
              "rel":"upcomingScheduledActivities",
              "href":"/v2/groups/acct/8a03fcae8dd65411b05f00505682315a/upcomingScheduledActivities"
            },
            {
              "rel":"horizontalAutoscalePolicyMapping",
              "href":"/v2/groups/acct/wa1-0002/horizontalAutoscalePolicy",
              "verbs":[
                "GET",
                "PUT",
                "DELETE"
              ]
            },
            {
              "rel": "scheduledActivities",
              "href": "/v2/groups/acct/8a03fcae8dd65411b05f00505682315a/scheduledActivities"
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
          "href": "/v2/groups/acct/wa1-0001"
        },
        {
          "rel": "parentGroup",
          "href": "/v2/groups/acct/wa1-0000",
          "id": "wa1-0000"
        },
        {
          "rel": "billing",
          "href": "/v2/groups/acct/wa1-0001/billing"
        },
        {
          "rel": "archiveGroupAction",
          "href": "/v2/groups/acct/wa1-0001/archive"
        },
        {
          "rel": "statistics",
          "href": "/v2/groups/acct/wa1-0001/statistics"
        },
        {
          "rel": "scheduledActivities",
          "href": "/v2/groups/acct/wa1-0001/scheduledActivities"
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
