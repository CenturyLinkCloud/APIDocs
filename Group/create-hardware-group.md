{{{
  "title": "Create Hardware Group",
  "date": "10-24-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

CreateHardwareGroup
<p>Creates a new Hardware Group.</p>
URL
<pre>REST: https://api.tier3.com/REST/Group/CreateHardwareGroup/&lt;format&gt;<br />SOAP: https://api.tier3.com/SOAP/Group.asmx?op=CreateHardwareGroup</pre> Request
<h3>Attributes</h3>
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
      <td>String</td>
      <td>The alias of the account to owns the group. Can be the parent alias or a sub-account alias.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ParentID</td>
      <td>Int</td>
      <td>The ID of the parent group.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Hardware Group</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>A description of the Hardware Group.If none is supplied, the Name will be used.</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>&nbsp;</pre>
<pre>  "AccountAlias": "UNK",

  "ParentID": "2",

  "Name": "Group 01",

  "Description": "My new group"

}</pre>
<h4>XML</h4>
<pre>&lt;CreateHardwareGroupRequest&gt;

    &lt;AccountAlias&gt;ACCT&lt;/AccountAlias&gt;

    &lt;ParentID&gt;2&lt;/ParentID&gt;

    &lt;Name&gt;Group 01&lt;/Name&gt;

    &lt;Description&gt;My new group&lt;/Description&gt;

&lt;/CreateHardwareGroupRequest&gt;</pre> Response
<h3>Attributes</h3>
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
      <td>Success</td>
      <td>Boolean</td>
      <td>True if the request was successful, otherwise False.</td>
    </tr>
    <tr>
      <td>Message</td>
      <td>String</td>
      <td>A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result.</td>
    </tr>
    <tr>
      <td>StatusCode</td>
      <td>Int</td>
      <td>This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state.</td>
    </tr>
    <tr>
      <td>Group</td>
      <td>Complex</td>
      <td>The created group (see below).</td>
    </tr>
  </tbody>
</table>
<h3>Group&nbsp;Attributes</h3>
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
      <td>ID</td>
      <td>Int</td>
      <td>The ID of the Group.</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Group.</td>
    </tr>
    <tr>
      <td>ParentID</td>
      <td>Int</td>
      <td>The ID of the Parent Group.</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{<br />    "Group":{"ID":5,"Name":"Group 01","ParentID":2},<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0<br />}</pre>
<h4>XML</h4>
<pre>&lt;CreateHardwareGroupResponse Success="true" Message="Success" StatusCode="0"&gt;<br />    &lt;Group ID="5" Name="Group 01" ParentID="2"/&gt;<br />&lt;/CreateHardwareGroupResponse&gt;</pre>
<h3>Status Codes</h3>
<table>
    <thead>
  <tr>
    <th>Status Code</th>
    <th>Description</th>
  </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;A Parent Group with the specified ID cannot be found.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1310</td>
      <td>The Name attribute is missing.</td>
    </tr>
  </tbody>
</table>