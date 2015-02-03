{{{
  "title": "Restore Hardware Group",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

RestoreHardwareGroup
<p>Restores an archived Hardware Group.</p>
URL
<pre>REST: https://api.tier3.com/REST/Group/RestoreHardwareGroup/&lt;format&gt;<br />SOAP: https://api.tier3.com/SOAP/Group.asmx?op=RestoreHardwareGroup</pre> Request
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
      <td>The alias of the account that owns the group. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access groups in your sub accounts.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>ID</td>
      <td>Int</td>
      <td>The ID of the hardware group to restore.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ParentID</td>
      <td>Int</td>
      <td>The ID of the hardware group to become the restored group's parent.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{

  "AccountAlias": "UNK",

  "ID": 1007,

  "ParentID": 1234

}</pre>
<h4>XML</h4>
<pre>&lt;RestoreGroupRequest&gt;

    &lt;AccountAlias&gt;ACCT&lt;/AccountAlias&gt;

    &lt;ID&gt;1004&lt;/ID&gt;

    &lt;ParentID&gt;1234&lt;/ParentID&gt;

&lt;/RestoreGroupRequest&gt;</pre>
<pre>&nbsp;</pre> Response
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
      <td>RequestID</td>
      <td>Int</td>
      <td>
        <p>The ID of the Queued request.</p>
        <p>Status of the request can be obtained by calling the&nbsp;<a href="http://help.tier3.com/entries/20561586-get-deployment-status">GetDeploymentStatus</a>&nbsp;method.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{<br />    "RequestID:1,<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0<br />}</pre>
<h4>XML</h4>
<pre>&lt;QueuedItemResponse Success="true" Message="Success" StatusCode="0"&gt;<br />&nbsp; &nbsp; &lt;RequestID&gt;1&lt;/RequestID&gt;<br />&lt;/QueuedItemResponse&gt;</pre>
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
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>
        <p>Resource Not Found. &nbsp;A Group with the specified ID cannot be found.&nbsp;</p>
      </td>
    </tr>
    <tr>
      <td>6</td>
      <td>
        <p>Invalid Operation. &nbsp;Group must be in an archived state.</p>
      </td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>