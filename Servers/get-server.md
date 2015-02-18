{{{
  "title": "Get Server",
  "date": "12-29-2014",
  "author": "Richard Seroter",
  "attachments": [],
  "sticky": "true"
}}}

Gets the details for a individual server. Calls to this operation must include a token acquired from the authentication endpoint. See the <a href="/api-docs/v2#authentication-login">Login API</a> for information on acquiring this token.

### When to Use It

Use this API operation when you want to find out all the details for a server. It can be used to look for changes, its status, or to retrieve links to associated resources.

### Supported HTTP Verbs

Requests to this endpoint are done via HTTP GET.

## URL

### Structure

    https://api.tier3.com/v2/servers/{accountAlias}/{serverId}

### Example

    https://api.tier3.com/v2/servers/ALIAS/WA1ACCTSERV0101

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
      <td>Short code for a particular account</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ServerId</td>
      <td>string</td>
      <td>ID of the server being queried. Retrieved from query to containing group, or by looking at the URL when viewing a server in the Control Portal.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

## Response

### Server Entity Definition

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
      <td>ID of the server being queried</td>
    </tr>
    <tr>
      <td>name</td>
      <td>string</td>
      <td>Name of the server</td>
    </tr>
    <tr>
      <td>description</td>
      <td>string</td>
      <td>User-defined description of this server</td>
    </tr>
    <tr>
      <td>groupId</td>
      <td>string</td>
      <td>ID of the parent group</td>
    </tr>
    <tr>
      <td>isTemplate</td>
      <td>boolean</td>
      <td>Boolean indicating whether this is a custom template or running server</td>
    </tr>
    <tr>
      <td>locationId</td>
      <td>string</td>
      <td>Data center that this server resides in</td>
    </tr>
    <tr>
      <td>osType</td>
      <td>string</td>
      <td>Friendly name of the Operating System the server is running</td>
    </tr>
    <tr>
      <td>status</td>
      <td>string</td>
      <td>Describes whether the server is active or not</td>
    </tr>
    <tr>
      <td>details</td>
      <td>complex</td>
      <td>Resource allocations, alert policies, snapshots, and more.</td>
    </tr>
    <tr>
      <td>type</td>
      <td>string</td>
      <td>Whether a standard or premium server</td>
    </tr>
    <tr>
      <td>storageType</td>
      <td>string</td>
      <td>Whether it uses standard or premium storage</td>
    </tr>
    <tr>
      <td>changeInfo</td>
      <td>complex</td>
      <td>Describes "created" and "modified" details</td>
    </tr>
    <tr>
      <td>links</td>
      <td>complex</td>
      <td>Collection of entity links that point to resources related to this server</td>
    </tr>
  </tbody>
</table>

### Details Definition

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
      <td>ipAddresses</td>
      <td>complex</td>
      <td>&nbsp;Details about IP addresses associated with the server</td>
    </tr>
    <tr>
      <td>alertPolicies</td>
      <td>complex</td>
      <td>Describe each alert policy applied to the server</td>
    </tr>
    <tr>
      <td>cpu</td>
      <td>integer</td>
      <td>How many vCPUs are allocated to the server</td>
    </tr>
    <tr>
      <td>diskCount</td>
      <td>integer</td>
      <td>How many disks are attached to the server</td>
    </tr>
    <tr>
      <td>hostName</td>
      <td>string</td>
      <td>Fully qualified name of the server</td>
    </tr>
    <tr>
      <td>inMaintenanceMode</td>
      <td>boolean</td>
      <td>Indicator of whether server has been placed in maintenance mode</td>
    </tr>
    <tr>
      <td>memoryMB</td>
      <td>integer</td>
      <td>How many MB of memory are allocated to the server</td>
    </tr>
    <tr>
      <td>powerState</td>
      <td>string</td>
      <td>Whether the server is running or not</td>
    </tr>
    <tr>
      <td>storageGB</td>
      <td>integer</td>
      <td>How many total GB of storage are allocated to the server</td>
    </tr>
    <tr>
      <td>snapshots</td>
      <td>complex</td>
      <td>Details about any snapshot associated with the server</td>
    </tr>
    <tr>
      <td>customFields</td>
      <td>&nbsp;complex</td>
      <td>Details about any custom fields and their values</td>
    </tr>
  </tbody>
</table>

### IPAddresses Definition

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
      <td>&nbsp;public</td>
      <td>string&nbsp;</td>
      <td>If applicable, the public IP</td>
    </tr>
    <tr>
      <td>internal</td>
      <td>string</td>
      <td>Private IP address. If associated with a public IP address, then the "public" value is populated</td>
    </tr>
  </tbody>
</table>

### AlertPolicies Definition

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
      <td>&nbsp;id</td>
      <td>string&nbsp;</td>
      <td>Unique identifier of the policy&nbsp;</td>
    </tr>
    <tr>
      <td>name</td>
      <td>string</td>
      <td>User-defined name of the alert policy</td>
    </tr>
    <tr>
      <td>links</td>
      <td>complex</td>
      <td>Collection of entity links that point to resources related to this policy</td>
    </tr>
  </tbody>
</table>

### AlertPolicies Links Definition

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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/policies/alerts/ID?account=[ALIAS]&amp;<br>location=WA1&amp;name=[SERVER]</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="3">Policy Map<br>Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">alertPolicyMap</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/servers/[ALIAS]/[SERVER]/alertPolicies/[ID]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the mapping to this server</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">verbs</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">array</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">DELETE</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Valid HTTP verbs that can act on this resource</td>
</tr>
</tbody>
</table>


### Snapshots Definition

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
      <td>name</td>
      <td>string&nbsp;</td>
      <td>Timestamp of the snapshot&nbsp;</td>
    </tr>
    <tr>
      <td>links</td>
      <td>complex</td>
      <td>Collection of entity links that point to resources related to this snapshot</td>
    </tr>
  </tbody>
</table>

<h3>Snapshot Links Definition</h3>

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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/servers/[ALIAS]/[<span>SERVER]</span>/snapshots/[ID]</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="2">Delete<br>Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">delete</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span>/v2/servers/[ALIAS]/[</span><span>SERVER]</span><span>/snapshots/[ID]</span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the snapshot for deletion</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="2">Restore<br>Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">restore</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span>/v2/servers/[ALIAS]/[</span><span>SERVER]</span><span>/snapshots/[ID]/restore</span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the snapshot for restoration</td>
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
      <td>Date/time that the server was created&nbsp;</td>
    </tr>
    <tr>
      <td>createdBy</td>
      <td>string</td>
      <td>Who created the server</td>
    </tr>
    <tr>
      <td>modifiedDate</td>
      <td>dateTime</td>
      <td>Date/time that the server was last updated</td>
    </tr>
    <tr>
      <td>modifiedBy</td>
      <td>string</td>
      <td>Who modified the server last</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="3">Self Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">self</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/servers/[ALIAS]/[SERVER]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the resource itself</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">verbs</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">array</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">GET | PATCH | DELETE</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span>Valid HTTP verbs that can act on this resource</span></td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="3">Group Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">group</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/groups/[ALIAS]/[GROUP]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the group</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">id</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">[GROUP]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Unique ID of the group</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="3">Account Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">account</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/accounts/[ALIAS]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the account</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">id</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">[ALIAS]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Unique ID of the account</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/servers/[ALIAS]/estimate-server/[SERVER]</span><span data-mce-mark="1"><br></span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of billing details &nbsp;for this server</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/servers/[ALIAS]/[SERVER]/</span><br><span data-mce-mark="1">statistics</span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of usage statistics for this server</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/servers/[ALIAS]/[SERVER]/</span><br><span data-mce-mark="1">scheduledActivities</span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the scheduled activities <br>(e.g.&nbsp;<span>restarts, pause) for this server</span></td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="3">Public IPs Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">publicIPAddresses</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/servers/[ALIAS]/[SERVER] /publicIPAddresses</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the resource itself</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">verbs</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">array</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">POST</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span>Valid HTTP verbs that can act on this resource</span></td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="3">Alert Policies Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">alertPolicyMappings</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/servers/[ALIAS]/[SERVER] /alertPolicies</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the resource itself</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">verbs</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">array</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">POST</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span>Valid HTTP verbs that can act on this resource</span></td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="3">Anti-Affinity Policies Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">antiAffinityPolicyMapping</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/servers/[ALIAS]/[SERVER] /antiAffinityPolicy</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the resource itself</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">verbs</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">array</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">PUT | DELETE</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span>Valid HTTP verbs that can act on this resource</span></td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="3">Autoscale Policy Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">cpuAutoscalePolicyMapping</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/servers/[ALIAS]/[SERVER] /cpuAutoscalePolicy</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the resource itself</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">verbs</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">array</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">PUT | DELETE</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span>Valid HTTP verbs that can act on this resource</span></td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="2">Capabilities Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">capabilities</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/servers/[ALIAS]/[SERVER] /capabilities</span><span data-mce-mark="1"><br></span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the capabilities resource</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="2">Credentials Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">credentials</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span data-mce-mark="1">/v2/servers/[ALIAS]/[SERVER] /credentials</span><span data-mce-mark="1"><br></span></td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the credentials resource</td>
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
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;" rowspan="4">IP Address Link</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">rel</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">publicIPAddress</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">The link type</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">href</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">/v2/servers/[ALIAS]/[SERVER] /publicIPAddresses /[IP ADDRESS]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Address of the resource itself</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">id</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">string</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">[IP ADDRESS]</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">Individual IP address</td>
</tr>
<tr>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">verbs</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">array</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;">GET | PUT | DELETE</td>
<td style="padding: 5px 5px 5px 5px; border: 1px solid gray;"><span>Valid HTTP verbs that can act on this resource</span></td>
</tr>
</tbody>
</table>


### Examples

#### JSON

```
{

  "id": "WA1ALIASWB01",

  "name": "WA1ALIASWB01",

  "description": "My web server",

  "groupId": "wa1-1002",

  "isTemplate": false,

  "locationId": "WA1",

  "osType": "Windows 2008 64-bit",

  "status": "active",

  "details": {

    "ipAddresses": [

      {

        "internal": "10.82.131.44"

      },

      {

        "public": "91.14.111.101",

        "internal": "10.82.131.45"

      }

    ],

    "alertPolicies": [

      {

        "id": "15836e6219e84ac736d01d4e571bb950",

        "name": "Production Web Servers - RAM",

        "links": [

          {

            "rel": "self",

            "href": "/v2/alertPolicies/alias/15836e6219e84ac736d01d4e571bb950"

          },

          {

            "rel": "alertPolicyMap",

            "href": "/v2/servers/alias/WA1ALIASWB01/alertPolicies/15836e6219e84ac736d01d4e571bb950"

",

            "verbs": [

              "DELETE"

            ]

          }

        ]

      },

      {

        "id": "2bec81dd90aa4217887548c3c20d7421"

        "name": "Production Web Servers - Disk",

        "links": [

          {

            "rel": "self",

            "href": "/v2/alertPolicies/alias/2bec81dd90aa4217887548c3c20d7421"

          },

          {

            "rel": "alertPolicyMap",

            "href": "/v2/servers/alias/WA1ALIASWB01/alertPolicies/2bec81dd90aa4217887548c3c20d7421"

",

            "verbs": [

              "DELETE"

            ]

          }

        ]

      }

    ],

    "cpu": 2,

    "diskCount": 1,

    "hostName": "WA1ALIASWB01.customdomain.com",

    "inMaintenanceMode": false,

    "memoryMB": 4096,

    "powerState": "started",

    "storageGB": 24,

    "snapshots": [

      {

        "name": "2014-05-16.23:45:52",

        "links": [

          {

            "rel": "self",

            "href": "/v2/servers/alias/WA1ALIASWB01/snapshots/40"

          },

          {

            "rel": "delete",

            "href": "/v2/servers/alias/WA1ALIASWB01/snapshots/40"

          },

          {

            "rel": "restore",

            "href": "/v2/servers/alias/WA1ALIASWB01/snapshots/40/restore"

          }

        ]

      }

    ],

    "customFields": [

      {

        "id": 22,

        "name": "Cost Center",

        "value": "IT-DEV",

        "displayValue": "IT-DEV"

      },

      {

        "id": 237,

        "name": "CMDB ID",

        "value": "1100003",

        "displayValue": "1100003"

      }

    ]

  },

  "type": "standard",

  "storageType": "standard",

  "changeInfo": {

    "createdDate": "2012-12-17T01:17:17Z",

    "createdBy": "user@domain.com",

    "modifiedDate": "2014-05-16T23:49:25Z",

    "modifiedBy": "user@domain.com"

  },

  "links": [

    {

      "rel": "self",

      "href": "/v2/servers/alias/WA1ALIASWB01",

      "id": "WA1ALIASWB01",

      "verbs": [

        "GET",

        "PATCH",

        "DELETE"

      ]

    },

    {

      "rel": "group",

      "href": "/v2/groups/alias/wa1-1002",

      "id": "wa1-3728"

    },

    {

      "rel": "account",

      "href": "/v2/accounts/alias",

      "id": "alias"

    },

    {

      "rel": "billing",

      "href": "/v2/billing/alias/estimate-server/WA1ALIASWB01"

    },

    {

      "rel": "statistics",

      "href": "/v2/servers/alias/WA1ALIASWB01/statistics"

    },

    {

      "rel": "scheduledActivities",

      "href": "/v2/servers/alias/WA1ALIASWB01/scheduledActivities"

    },

    {

      "rel": "publicIPAddresses",

      "href": "/v2/servers/alias/WA1ALIASWB01/publicIPAddresses",

      "verbs": [

        "POST"

      ]

    },

    {

      "rel": "alertPolicyMappings",

      "href": "/v2/servers/alias/WA1ALIASWB01/alertPolicies",

      "verbs": [

        "POST"

      ]

    },

    {

      "rel": "antiAffinityPolicyMapping",

      "href": "/v2/servers/alias/WA1ALIASWB01/antiAffinityPolicy",

      "verbs": [

        "DELETE",

        "PUT"

      ]

    },

    {

      "rel": "cpuAutoscalePolicyMapping",

      "href": "/v2/servers/alias/WA1ALIASWB01/cpuAutoscalePolicy",

      "verbs": [

        "DELETE",

        "PUT"

      ]

    },

    {

      "rel": "capabilities",

      "href": "/v2/servers/alias/WA1ALIASWB01/capabilities"

    },

    {

      "rel": "credentials",

      "href": "/v2/servers/alias/WA1ALIASWB01/credentials"

    },

    {

      "rel": "publicIPAddress",

      "href": "/v2/servers/alias/WA1ALIASWB01/publicIPAddresses/91.14.111.101",

      "id": "91.14.111.101",

      "verbs": [

        "GET",

        "PUT",

        "DELETE"

      ]

    }

  ]

}
```
