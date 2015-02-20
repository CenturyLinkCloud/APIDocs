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

    GET https://api.tier3.com/v2/groups/ALIAS/wa1-5030

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
      <td>serverCount</td>
      <td>integer</td>
      <td>Number of servers this group contains</td>
    </tr>
    <tr>
      <td>Groups</td>
      <td>array</td>
      <td>Refers to this same entity type for each sub-group</td>
    </tr>
    <tr>
      <td>Links</td>
      <td>array</td>
      <td>Collection of entity links that point to resources related to this group</td>
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

### Activities Link Definition

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

### Examples

#### JSON

    {
      "id": "wa1-0001",
      "name": "Web Applications",
      "description": "public facing web apps",
      "type": "default",
      "status": "active",
      "serversCount": 2,
      "groups": [
        {
          "id": "wa1-0002",
          "name": "Training Environment",
          "description": "Temporary servers",
          "type": "default",
          "status": "active",
          "serversCount": 0,
          "groups": [],
          "links": [
            {
              "rel": "self",
              "href": "/v2/groups/acct/wa1-0002"
            },
            {
              "rel": "delete",
              "href": "/v2/groups/acct/wa1-0002"
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
              "rel": "scheduledActivities",
              "href": "/v2/groups/acct/wa1-0002/scheduledActivities"
            }
          ]
        }
      ],
      "links": [
        {
          "rel": "self",
          "href": "/v2/groups/acct/wa1-0001"
        },
        {
          "rel": "delete",
          "href": "/v2/groups/acct/wa1-0001"
        },
        {
          "rel": "parentGroup",
          "href": "/v2/groups/acct/wa1-0000",
          "id": "wa1-3728"
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
      ]
    }
