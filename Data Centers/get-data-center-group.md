{{{
  "title": "Get Data Center Group",
  "date": "5-16-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the full hierarchy of groups that exist within a particular account and data center. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to discover the name of the root hardware group for a data center. Once you have that group alias, you can issue a secondary query to retrieve the entire group hierarchy for a given data center.

### Supported HTTP Verbs

Requests to this endpoint are done via HTTP GET.

## URL

### Structure

    https://api.tier3.com/v2/datacenters/{accountAlias}/{dataCenter}?groupLinks=true|false

### Example

    https://api.tier3.com/v2/datacenters/ALIAS/UC1?groupLinks=true

## Request

### URI and Querystring Parameters

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
      <td>Short code for a particular account</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>DataCenter</td>
      <td>string</td>
      <td>Short string representing the data center you are querying. Valid codes can be retrieved from the&nbsp;<strong>List Data Centers</strong> API operation.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>GroupLinks</td>
      <td>boolean</td>
      <td>Determine whether link collections are returned for each group</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

## Response

### Entity Definition

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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/datacenters/[ALIAS]/[DC]</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="4">Group Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">group</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/datacenters/[ALIAS]/[DC]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the root hardware group</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">id</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">[GROUPID]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Identifier of the root hardware group</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">name</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">[GROUP NAME]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Friendly name of the group</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/datacenters/[ALIAS]/[GROUPID]/<br>billing</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the billing information for the group</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/datacenters/[ALIAS]/[GROUPID]/</span><br><span data-mce-mark="1">archive</span></td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/datacenters/[ALIAS]/[GROUPID]/</span><br><span data-mce-mark="1">statistics</span></td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/datacenters/[ALIAS]/[GROUPID]/</span><br><span data-mce-mark="1">scheduledActivities</span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the scheduled activities <br>(e.g.&nbsp;<span>restarts, pause) for this group</span></td>
</tr>
</tbody>
</table>

### Examples

#### JSON

    {
      "id": "DC1",
      "name": "DC FRIENDLY NAME",
      "links": [
        {
          "rel": "self",
          "href": "/v2/datacenters/ALIAS/DC1"
        },
        {
          "rel": "group",
          "href": "/v2/groups/ALIAS/GROUP123",
          "id": "groupid",
          "name": "DC1 Hardware"
        },
        {
          "rel": "billing",
          "href": "/v2/groups/ALIAS/GROUP123/billing"
        },
        {
          "rel": "archiveGroupAction",
          "href": "/v2/groups/ALIAS/GROUP123/archive"
        },
        {
          "rel": "statistics",
          "href": "/v2/groups/ALIAS/GROUP123/statistics"
        },
        {
          "rel": "scheduledActivities",
          "href": "/v2/groups/ALIAS/GROUP123/scheduledActivities"
        }
      ]
    }
