{{{
  "title": "Get Blueprints",
  "date": "9-26-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets a list of all Blueprints with the specified search criteria.

## URL

    REST:https://api.tier3.com/REST/Blueprint/GetBlueprints/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Blueprints.asmx?op=GetBlueprintsResponseMsg

## Request
### Attributes
<table>
    <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Required</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>CompanySize</td>
      <td>Int</td>
      <td>
        <p>The target company size the of the Blueprint</p>
        <p>1 = 1 - 100
          <br />2 = 101 - 1,000
          <br />3 = 1,001 - 5,000
          <br />4 = &nbsp;5,000+</p>
      </td>
      <td>
        <p>No</p>
      </td>
    </tr>
    <tr>
      <td>OperatingSystems</td>
      <td>Int[]</td>
      <td>
        <p>A list of the operating systems that a Blueprint contains</p>
        <p>Cent OS - 32 bit = 6
          <br />Cent OS - 64 bit = 7
          <br />Debian - 64 bit = 21
          <br />Free BSD - 32 bit = 13
          <br />Free BSD - 64 bit = 14
          <br />Ubuntu - 32 bit = 19
          <br />Ubuntu - 64 bit = 20
          <br />Windows 2003 Enterprise - 32 bit = 15
          <br />Windows 2003 Enterprise - 64 bit = 16
          <br />Windows 2003 - 32 bit = 2
          <br />Windows 2003 - 64 bit = 3
          <br />Windows 2008 - 32 bit = 4
          <br />Windows 2008 - 64 bit = 5
          <br />Windows 2008 Enterprise - 32 bit = 17
          <br />Windows 2008 Enterprise - 64 bit = 18</p>
      </td>
      <td>&nbsp;No</td>
    </tr>
    <tr>
      <td>Search</td>
      <td>String</td>
      <td>
        <p>A keyword search within the Name and Description of the Blueprint&nbsp;</p>
      </td>
      <td>
        <p>No</p>
      </td>
    </tr>
    <tr>
      <td>Visibility</td>
      <td>Int</td>
      <td>
        <p>The visibility level of the Blueprint</p>
        <p>1 = Public
          <br />2 = Private
          <br />3 = Private Shared</p>
      </td>
      <td>
        <p>No</p>
      </td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{ <br />    "CompanySize": "2",&nbsp;<br />    "OperatingSystems": [ 4, 5, 17, 18],<br />    "Search": "High Performance",<br />    "Visibility": 1<br />}</pre>

<h4>XML</h4>
<pre>&lt;GetBlueprintsRequest&gt;<br />    &lt;CompanySize&gt;2&lt;/CompanySize&gt;<br />    &lt;OperatingSystems&gt;<br />        &lt;OS&gt;4&lt;/OS&gt;<br />        &lt;OS&gt;5&lt;/OS&gt;<br />        &lt;OS&gt;17&lt;/OS&gt;<br />        &lt;OS&gt;18&lt;/OS&gt;<br />    &lt;/OperatingSystems&gt;<br />    &lt;Search&gt;High Performance&lt;/Search&gt;<br />    &lt;Visibility&gt;1&lt;/Visibility&gt;<br />&lt;/GetBlueprintsRequest&gt;&nbsp;</pre>

## Response
### Attributes
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
      <td>Blueprints</td>
      <td>Complex (see below)</td>
      <td>A list of Blueprints (see below)</td>
    </tr>
  </tbody>
</table>

### Blueprint Attributes
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
      <td>The ID of the Blueprint.</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Blueprint.</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{<br />    "Blueprints":[<br />        {"ID":1,"Name":"Blueprint 01"},<br />        {"ID":2,"Name":"Blueprint 02"},<br />    ],    <br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0<br />}</pre>

<h4>XML</h4>
<pre>&lt;GetBlueprintsResponse Success="true" Message="Success" StatusCode="0"&gt;<br />    &lt;Blueprints&gt;<br />        &lt;Blueprint ID="1" Name="Blueprint 01" /&gt;<br />        &lt;Blueprint ID="2" Name="Blueprint 02" /&gt;<br />    &lt;/Blueprints&gt;<br />&lt;/GetBlueprintsResponse&gt;</pre>

### Status Codes
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
      <td>1201</td>
      <td>The Visibility value is missing or invalid.</td>
    </tr>
  </tbody>
</table>