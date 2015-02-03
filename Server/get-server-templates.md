{{{
  "title": "GetServerTemplates",
  "date": "8-20-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the list of Templates available to the account.

## URL

    REST: https://api.tier3.com/REST/Server/GetServerTemplates/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Server.asmx?op=GetServerTemplates

## Request
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
      <td>Templates</td>
      <td>Complex</td>
      <td>A list of <a href="/entries/23104781-Server-Template-Object" target="_blank">Server Template Objects</a>
      </td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{<br />    "RequestID:1,<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0,<br />    "Templates":[

        {

            "ID":1001,"Name":"CENTOS-6-32","Description":"Cent OS 6 | 32-bit",

            "Cpu":1,"MemoryGB":2 "DiskCount":1 "TotalDiskSpaceGB":8 "OperatingSystem":6

        },

        {

            "ID":1002,"Name":"WIN2008R2STD-64","Description":"Windows 2008 R2 Standard | 64-bit",

            "Cpu":1,"MemoryGB":4 "DiskCount":1 "TotalDiskSpaceGB":16 "OperatingSystem":18

        }

     ]

}</pre>

<h4>XML</h4>
<pre>&lt;GetTemplatesResponse Success="true" Message="Successfully retrieved templates" StatusCode="0"&gt;

    &lt;Templates&gt;

        &lt;Template ID="1001" Name="CENTOS-6-32" Description="CentOS 6 | 32-bit" Cpu="1"

        MemoryGB="2" DiskCount="1" TotalDiskSpaceGB="8" OperatingSystem="6" /&gt;

        &lt;Template ID="1001" Name="WIN2008R2STD-64" Description="Windows 2008 R2 Standard | 64-bit" 

        Cpu="1" MemoryGB="4" DiskCount="1" TotalDiskSpaceGB="16" OperatingSystem="18" /&gt;

    &lt;/Templates&gt;

&lt;/GetTemplatesResponse&gt;</pre>

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
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>