{{{
  "title": "Get Group",
  "date": "10-15-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the details for a individual server group and any sub-groups and servers that it contains. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to identify the servers in a particular group, retrieve a group hierarchy, or get links to information (e.g. billing, monitoring, scheduled activities) about a group.

### Supported HTTP Verbs

Requests to this endpoint are done via HTTP GET.

## URL

### Structure

    https://api.tier3.com/v2/groups/{accountAlias}/{groupId}

### Example

    https://api.tier3.com/v2/groups/ALIAS/wa1-5030

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
      <td>Short code for a particular account.&nbsp;</td>
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
      <td>Limits</td>
      <td>complex</td>
      <td>Group-based resource limits</td>
    </tr>
    <tr>
      <td>Groups</td>
      <td>array</td>
      <td>&nbsp;Refers to this same entity type for each sub-group</td>
    </tr>
    <tr>
      <td>Links</td>
      <td>array</td>
      <td>Collection of entity links that point to resources related to this group</td>
    </tr>
  </tbody>
</table>

### Limits Definition

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
      <td>cpu</td>
      <td>integer</td>
      <td>How many CPUs can be deployed to servers in this group</td>
    </tr>
    <tr>
      <td>memoryGB</td>
      <td>integer</td>
      <td>How much memory can be deployed to servers in this group</td>
    </tr>
    <tr>
      <td>storageGB</td>
      <td>integer</td>
      <td>How much storage can be deployed to servers in this group</td>
    </tr>
  </tbody>
</table>

### Links Definition

<table style="border: 1px solid gray; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>Name</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="75"><strong>Type</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="250"><strong>Value</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="2">Self Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">self</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/groups/[ALIAS]/[GROUPID]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the resource itself</td>
</tr>
</tbody>
</table>


<table style="border: 1px solid gray; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>Name</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="75"><strong>Type</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="250"><strong>Value</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="3">Parent Group<br>Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">parentGroup</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/groups/[ALIAS]/[GROUPID]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the parent group</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">id</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">[GROUPID]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Unique ID of the parent group</td>
</tr>
</tbody>
</table>


<table style="border: 1px solid gray; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>Name</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="75"><strong>Type</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="250"><strong>Value</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="2">Billing Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">billing</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/groups/[ALIAS]/[GROUPID]/<br>billing</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the billing information for the grou</td>
</tr>
</tbody>
</table>


<table style="border: 1px solid gray; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>Name</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="75"><strong>Type</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="250"><strong>Value</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="2">Archive Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">archiveGroupAction</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/groups/[ALIAS]/[GROUPID]/</span><br><span data-mce-mark="1">archive</span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the archive details for this group</td>
</tr>
</tbody>
</table>


<table style="border: 1px solid gray; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>Name</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="75"><strong>Type</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="250"><strong>Value</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="2">Statistics Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">statistics</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/groups/[ALIAS]/[GROUPID]/</span><br><span data-mce-mark="1">statistics</span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of usage statistics for this group</td>
</tr>
</tbody>
</table>


<table style="border: 1px solid gray; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>Name</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="75"><strong>Type</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="250"><strong>Value</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="2">Activities Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">scheduledActivities</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/groups/[ALIAS]/[GROUPID]/</span><br><span data-mce-mark="1">scheduledActivities</span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the scheduled activities <br>(e.g.&nbsp;<span>restarts, pause) for this group</span></td>
</tr>
</tbody>
</table>


<table style="border: 1px solid gray; border-collapse: collapse;">
<tbody>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>&nbsp;</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="100"><strong>Name</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="75"><strong>Type</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="250"><strong>Value</strong></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" width="300"><strong>Description</strong></td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="3">Server Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">server</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/servers/[ALIAS]/[SERVERID]</span><span data-mce-mark="1"><br></span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the server<span>&nbsp;in this group</span></td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">id</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">[SERVERID]</span><span data-mce-mark="1"><br></span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span>ID of the server in this group</span></td>
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

      "limits": {

        "cpu": 80,

        "memoryGB": 160,

        "storageGB": 4096

      },

      "groups": [

        {

          "id": "wa1-0002",

          "name": "Training Environment",

          "description": "Temporary servers",

          "type": "default",

          "status": "active",

          "serversCount": 0,

          "limits": {

            "cpu": 80,

            "memoryGB": 160,

            "storageGB": 4096

          },

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