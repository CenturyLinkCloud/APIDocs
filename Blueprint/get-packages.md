{{{
  "title": "Get Packages",
  "date": "11-24-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

GetPackages
<p>Gets a list of Blueprint Packages.</p>
URL
<pre>REST: <code>https://api.tier3.com/REST/Blueprint/GetPackages/&lt;format&gt;</code><br />SOAP: <code>https://api.tier3.com/SOAP/Blueprints.asmx?op=GetPackagesResponseMsg</code></pre> Request
<h3>Attributes</h3>
<table>
  <tbody>
    <tr>
      <td><strong>Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Description</strong>
      </td>
      <td><strong>Required</strong>
      </td>
    </tr>
    <tr>
      <td>Classification</td>
      <td>Int</td>
      <td>
        <p>The type of Packages that should be returned</p>
        <p>1 = System
          <br />2 = Script
          <br />3 = Software</p>
      </td>
      <td>
        <p>Yes</p>
      </td>
    </tr>
    <tr>
      <td>Visibility</td>
      <td>Int</td>
      <td>
        <p>The visibility of Packages that should be returned</p>
        <p>1 = Public
          <br /> 2 = Private
          <br /> 3 = Shared</p>
      </td>
      <td>
        <p>Yes</p>
      </td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{ "Classification": "1", "Visibility": "1" }&nbsp;</pre>
<h4>XML</h4>
<pre>&lt;GetPackagesRequest&gt;<br />&nbsp; &nbsp; &lt;Classification&gt;1&lt;/Classification&gt;&nbsp;<br />&nbsp; &nbsp; &lt;Visibility&gt;1&lt;/Visibility&gt;<br />&lt;/GetPackagesRequest&gt;&nbsp;</pre> Response
<h3>Attributes</h3>
<table>
  <tbody>
    <tr>
      <td><strong>Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
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
      <td>Complex</td>
      <td>
        <p>A list of Packages (see below)</p>
      </td>
    </tr>
  </tbody>
</table>
<h3>Package Attributes</h3>
<table>
  <tbody>
    <tr>
      <td><strong>Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
    <tr>
      <td>ID</td>
      <td>Int</td>
      <td>The ID of the Package. &nbsp;This value is for reference only.</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Package.</td>
    </tr>
    <tr>
      <td>Classifcation</td>
      <td>Int</td>
      <td>
        <p>The&nbsp;classification&nbsp;of the Package.</p>
        <p>1 = System
          <br />2 = Script
          <br />3 = Software&nbsp;</p>
      </td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{<br />&nbsp; &nbsp; "Packages": [<br />&nbsp; &nbsp; &nbsp; &nbsp; {"ID":2,"Name":"Add Disk","Classification":1},<br />&nbsp; &nbsp; &nbsp; &nbsp; {"ID":3,"Name":"Add IP Address","Classification":1},<br />&nbsp; &nbsp; &nbsp; &nbsp; {"ID":4,"Name":"Add Mapped IP Address","Classification":1},<br />&nbsp; &nbsp; &nbsp; &nbsp; {"ID":5,"Name":"Snapshot Server","Classification":1},<br />&nbsp; &nbsp; &nbsp; &nbsp; {"ID":6,"Name":"Reboot Server","Classification":1}<br />&nbsp; &nbsp; ],<br />&nbsp; &nbsp; "Success":true,<br />&nbsp; &nbsp; "Message":"Success",<br />&nbsp; &nbsp; "StatusCode":0<br />}</pre>
<h4>XML</h4>
<div>
  <div>
    <pre>&lt;GetPackagesResponse Success="true" Message="Success" StatusCode="0"&gt;<br />&nbsp; &nbsp; &lt;Packages&gt;<br />&nbsp; &nbsp; &nbsp; &nbsp;  &lt;Package ID="2" Name="Add Disk" Classification="1" /&gt;<br /> &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&lt;Package ID="3" Name="Add IP Address" Classification="1" /&gt;<br /> &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&lt;Package ID="4" Name="Add Mapped IP Address" Classification="1" /&gt;<br /> &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&lt;Package ID="5" Name="Snapshot Server" Classification="1" /&gt;<br /> &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&lt;Package ID="6" Name="Reboot Server" Classification="1" /&gt;<br />&nbsp; &nbsp; &lt;/Packages&gt;<br />&lt;/GetPackagesResponse&gt;</pre>
  </div>
</div>
<h4>Status Codes</h4>
<table>
  <tbody>
    <tr>
      <td><strong>Status Code</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
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
    <tr>
      <td>1200</td>
      <td>The Classification value is missing or invalid.</td>
    </tr>
    <tr>
      <td>1201</td>
      <td>The Visibility value is missing or invalid.</td>
    </tr>
  </tbody>
</table>