{{{
  "title": "GetArchiveServers",
  "date": "2-28-2012",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the list of Archive Servers.

## URL

    REST: https://api.tier3.com/REST/Server/GetArchiveServers/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Server.asmx?op=GetArchiveServers

## Request
### Attribute
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
      <td>Servers</td>
      <td>Complex (see below)</td>
      <td>
        <p>A list of Archive Servers (see below)</p>
      </td>
    </tr>
  </tbody>
</table>

### Archive Server Attributes
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
      <td>The ID of the Server.</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The full name of the Server.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>The description of the Server as provided on creation.</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0,<br />    "Servers":[<br />        {"ID":1001,"Name":"WA1T3NWEB01","Description":"WA1T3NWEB01"},<br />        {"ID":1002,"Name":"WA1T3NWEB02","Description":"WA1T3NWEB02"}<br />     ]<br />}</pre>

<h4>XML</h4>
<pre>&lt;GetServersResponse Success="true" Message="Successfully retrieved servers" StatusCode="0"&gt;<br />    &lt;Servers&gt;<br />        &lt;Server ID="1001" Name="WA1T3NWEB01" Description="WA1T3NWEB01"/&gt;<br />        &lt;Server ID="1002" Name="WA1T3NWEB02" Description="WA1T3NWEB02"/&gt;<br />    &lt;/Servers&gt;&nbsp;<br />&lt;/GetServersResponse&gt;</pre>

### Status Codes
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
      <td>Resource Not Found. &nbsp;The archive group could not be found. &nbsp;Please contact <a href="mailto:noc@tier3.com">noc@tier3.com</a>.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>