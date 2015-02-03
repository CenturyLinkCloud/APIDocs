{{{
  "title": "Get Pending Packages",
  "date": "12-2-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets a list of Blueprint Packages that are pending publication.

This list contains all Packages that were uploaded to Tier 3 via FTP or that were uploaded in the UI via HTTP.

## URL

    REST: https://api.tier3.com/REST/Blueprint/GetPendingPackages/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Blueprints.asmx?op=GetPendingPackages

## Request
### Attributes
None.

## Response
### Attributes
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
      <td>Packages</td>
      <td>Complex (see below)</td>
      <td>
        <p>A list of Packages (see below)</p>
      </td>
    </tr>
  </tbody>
</table>

### Package Attributes
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
      <td>
        <p>The ID of the Package. &nbsp;</p>
        <p>This value is for reference only and will always be 0.</p>
      </td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>
        <p>The name of the Package.</p>
        <p>This will be the name of the Package zip file that was uploaded.</p>
      </td>
    </tr>
    <tr>
      <td>Classification</td>
      <td>Int</td>
      <td>
        <p>This value will always be 0 for pending packages</p>
      </td>
    </tr>
  </tbody>
</table>

### Examples

<h4>JSON</h4>
<pre>{<br />&nbsp; &nbsp; "Packages": [<br />&nbsp; &nbsp; &nbsp; &nbsp; {"ID":0,"Name":"Script 01","Classification":0},<br />&nbsp; &nbsp; &nbsp; &nbsp; {"ID":0,"Name":"Software 01","Classification":0}<br />&nbsp; &nbsp; ],<br />&nbsp; &nbsp; "Success":true,<br />&nbsp; &nbsp; "Message":"Success",<br />&nbsp; &nbsp; "StatusCode":0<br />}</pre>

<h4>XML</h4>

<pre>&lt;GetPackagesResponse Success="true" Message="Success" StatusCode="0"&gt;<br />&nbsp; &nbsp; &lt;Packages&gt;<br />&nbsp; &nbsp; &nbsp; &nbsp;  &lt;Package ID="0" Name="Script 01" Classification="0" /&gt;<br /> &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&lt;Package ID="0" Name="Software 01" Classification="0" /&gt;<br />&nbsp; &nbsp; &lt;/Packages&gt;<br />&lt;/GetPackagesResponse&gt;</pre>

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
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>
