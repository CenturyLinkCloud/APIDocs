{{{
  "title": "GetAllServersByModifiedDates",
  "date": "12-26-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

GetAllServersByModifiedDates
<p>Gets a deep list of all modified Servers for a given Hardware Group and its sub groups, or all Servers&nbsp;for&nbsp;a given location. To get all servers that have changed since a certain date, only provide a BeginDate and omit the EndDate.</p>
URL
<pre>REST: https://api.tier3.com/REST/Server/GetAllServersByModifiedDates/&lt;format&gt;<br />SOAP: https://api.tier3.com/SOAP/Server.asmx?op=GetAllServersByModifiedDatesResponseMsg</pre> Request
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
      <td>AccountAlias</td>
      <td>String</td>
      <td>The alias of the account that owns the servers. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to query a particular sub-account.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>HardwareGroupID</td>
      <td>Int</td>
      <td>The ID of the Hardware Group, or 0 if providing Location.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>The data center location.&nbsp; Otherwise leave blank and provide HardwareGroupID or let it default to account's primary data center.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>BeginDate</td>
      <td>DateTime</td>
      <td>Beginning of date range for querying modified servers. Can be a partial DateTime (e.g. 2013-05-10) or a full DateTime (e.g. 2013:05-10T14:30:12). If date is missing, then the value equals today minus one day.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>EndDate</td>
      <td>DateTime</td>
      <td>End of date range for querying modified servers. Can be a partial DateTime (e.g. 2013-05-10) or a full DateTime (e.g. 2013:05-10T14:30:12). If date is missing, then the value is set to the current date time.&nbsp;</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{ <br />   "AccountAlias": "ACCT", <br />   "Location": "WA1",<br />   "BeginDate": "2013-05-01",<br />   "EndDate": "2013-06-30"<br /> }</pre>
<h4>XML</h4>
<pre>&lt;GetAllServersRequest&gt;

    &lt;AccountAlias&gt;ACCT&lt;/AccountAlias&gt;

    &lt;Location&gt;WA1&lt;/Location&gt;<br />    &lt;BeginDate&gt;2013-05-01&lt;/BeginDate&gt;<br />    &lt;EndDate&gt;2013-06-30&lt;/EndDate&gt;

&lt;/GetAllServersRequest&gt;&nbsp;</pre> Response
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
      <td>Servers</td>
      <td>Complex</td>
      <td>A list of&nbsp;<a href="/entries/23105126-Server-Object" target="_blank">Server Objects</a>
      </td>
    </tr>
  </tbody>
</table>
<h3><a href="/entries/23105126-Server-Object" target="_blank">Server&nbsp;Object&nbsp;description</a></h3>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0,<br />    "Servers":[<br />        {"ID":1001,"HardwareGroupID":1,"Name":"WA1T3NWEB01","Description":"WA1T3NWEB01",<br />            "DnsName":"WA1T3NWEB01","IsTemplate":false,"Cpu":2,"MemoryGB":4,"DiskCount":3,<br />            "TotalDiskSpaceGB":116,"Status":"Active","ServerType":"2","ServiceLevel":"1",<br />            "OperatingSystem":4,"PowerState":"Started","Location":"WA1","IPAddress":"172.0.0.1"<br />            "IPAddresses:[<br />                {"Address":"172.0.01", "AddressType":1}<br />            ],"CustomFields":[<br />                { "CustomFieldID": 100,"Name": "My Field", "Type": "Text", "Value": "A test"},<br />                { "CustomFieldID": 101,"Name": "My Field 2","Type": "Option","Value": "2"},<br />                { "CustomFieldID": 102,"Name": "My Field 3","Type": "Checkbox","Value": "true"},]},<br /><br />        {"ID":1002,"HardwareGroupID":1,"Name":"WA1T3NWEB02","Description":"WA1T3NWEB02",<br />            "DnsName":"WA1T3NWEB02","IsTemplate":false,"Cpu":2,"MemoryGB":4,"DiskCount":3,<br />            "TotalDiskSpaceGB":116,"Status":"Active","ServerType":"1","ServiceLevel":"2",<br />            "OperatingSystem":6,"PowerState":"Started","Location":"WA1","IPAddress":"172.0.0.2"<br />            "IPAddresses:[<br />                {"Address":"172.0.02", "AddressType":1}<br />            ], "CustomFields": [] }<br />     ]<br />}</pre>
<h4>XML</h4>
<pre>&lt;GetServersResponse Success="true" Message="Successfully retrieved servers" StatusCode="0"&gt;<br />    &lt;Servers&gt;<br />        &lt;Server ID="1001" HardwareGroupID="1" Name="WA1T3NWEB01" Description="WA1T3NWEB01" <br />                DnsName="WA1T3NWEB01" IsTemplate="false" Cpu="2" MemoryGB="4" DiskCount="3" <br />                TotalDiskSpaceGB="116" Status="Active" ServerType="1" ServiceLevel="2" <br />                OperatingSystem="2" PowerState="Started" Location="WA1" IPAddress="172.0.0.1"&gt;<br />            &lt;IPAddresses&gt;<br />                &lt;IPAddress Address="172.0.0.1" AddressType="RIP" /&gt;<br />            &lt;/IPAddresse&gt;<br />            &lt;CustomFields CustomFieldID="100" Name="My Field" Type="Text" Value="Test Value" /&gt;<br />            &lt;CustomFields CustomFieldID="101" Name="My 2nd Field" Type="Option" Value="Value 3" /&gt;<br />            &lt;CustomFields CustomFieldID="102" Name="My 3rd Field" Type="Checkbox" Value="true" /&gt;<br />        &lt;/Server&gt;<br />        &lt;Server ID="1002" HardwareGroupID="1" Name="WA1T3NWEB02" Description="WA1T3NWEB02" <br />                DnsName="WA1T3NWEB02" IsTemplate="false" Cpu="2" MemoryGB="4" DiskCount="3" <br />                TotalDiskSpaceGB="116" Status="Active"&nbsp;ServerType="2" ServiceLevel="1" <br />                OperatingSystem="6" PowerState="Started" Location="WA1" IPAddress="172.0.0.2"<br />            &lt;IPAddresses&gt;<br />                &lt;IPAddress Address="172.0.0.2" AddressType="RIP"/&gt;<br />            &lt;/IPAddresses&gt;<br />            &lt;CustomFields /&gt;<br />       &lt;/Server&gt;<br />    &lt;/Servers&gt;&nbsp;<br />&lt;/GetServersResponse&gt;</pre>
<h3>Status Codes</h3>
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
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;A Group with the specified ID cannot be found.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>