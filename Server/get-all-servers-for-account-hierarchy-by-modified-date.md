{{{
  "title": "Get All Servers For AccountHierarchy By ModifiedDate",
  "date": "6-28-2013",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets a deep list of all modified servers for a given account hierarchy within a given data center. Use this operation to get a full list of all servers contained within an account and all its subaccounts.&nbsp;To get all servers that have changed since a certain date, only provide a BeginDate and omit the EndDate.

## URL

    REST: https://api.tier3.com/REST/Server/GetAllServersForAccountHierarchyByModifiedDates/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Server.asmx?op=GetAllServersForAccountHierarchyByModifiedDatesMsg

## Request
### Attributes
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
      <td>The alias of the account that owns the servers. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to query a particular sub-account.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>HardwareGroupID</td>
      <td>Int</td>
      <td>Ignored</td>
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

### Examples
<h4>JSON</h4>
<pre>{ <br />   "AccountAlias": "ACCT", <br />   "Location": "WA1",<br />   "BeginDate": "2013-05-01",<br />   "EndDate": "2013-06-30"<br /> }</pre>

<h4>XML</h4>
<pre>&lt;GetAllServersByModifiedDatesRequest&gt;

    &lt;AccountAlias&gt;ACCT&lt;/AccountAlias&gt;

    &lt;Location&gt;WA1&lt;/Location&gt;<br />    &lt;BeginDate&gt;2013-05-01&lt;/BeginDate&gt;<br />    &lt;EndDate&gt;2013-06-30&lt;/EndDate&gt;

&lt;/GetAllServersByModifiedDatesRequest&gt;&nbsp;</pre>

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
      <td>Servers</td>
      <td>Complex</td>
      <td>A list of AccountServerGroups, each containing&nbsp;<a href="/entries/23105126-Server-Object" target="_blank">Server Objects</a>
      </td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{"AccountServers":[

    {"AccountAlias":"ACT1","Servers":[

        {"ID":2646,"HardwareGroupID":1197,"Location":"WA1","Name":"SERVERDEMO01","Description":"Demo server",

            "DnsName":"", "IsTemplate":false,"Cpu":1,"MemoryGB":2,"DiskCount":1,"TotalDiskSpaceGB":24,

            "Status":"UnderConstruction","PowerState":"Stopped","InMaintenanceMode":false,

            "IPAddress":"","ServerType":1,"ServiceLevel":2,"OperatingSystem":18,

            "DateModified":"\/Date(1347577422943)\/","ModifiedBy":"user@tier3.com",

            "IPAddresses":[

                {"Address":"142.25.114.13","AddressType":"RIP"}],

            "CustomFields":null},

        {"ID":3015," HardwareGroupID":1111,"Location":"WA1","Name":"SERVERDEMO02","Description":"Demo server",

            "DnsName":null,"IsTemplate":false,"Cpu":0,"MemoryGB":0,"DiskCount":0,"TotalDiskSpaceGB":0,

            "Status":"Deleted"," PowerState":"Stopped", "InMaintenanceMode":false,

            "IPAddress":null,"ServerType":1,"ServiceLevel":2,"OperatingSystem":5,

            "DateModified":"\/Date(1355446615983)\/","ModifiedBy":"user@tier3.com",

            "IPAddresses":[],"CustomFields":null}]},

    {"AccountAlias":"ACT2","Servers":[

        {"ID":4316,"HardwareGroupID":1595,"Location":"WA1","Name":"SERVERDEMO03","Description":"demo server",\

            "DnsName":"QA1SSUBSERO9401","IsTemplate":false,"Cpu":1,"MemoryGB":1,"DiskCount":3,"TotalDiskSpaceGB":17,

            "Status":"Active","PowerState":"Started","InMaintenanceMode":false,

            "IPAddress":"173.25.114.15","ServerType":1,"ServiceLevel":2,"OperatingSystem":20,

            "DateModified":"\/Date(1372476852953)\/","ModifiedBy":"user@tier3.com",

            "IPAddresses":[

                {"Address":"173.25.114.15","AddressType":"RIP"}],

            "CustomFields":null}]}],

    "Success":true,"Message":"Successfully retrieved deep view of servers","StatusCode":0}

</pre>

<h4>XML</h4>
<pre>&lt;GetAccountHierarchyServersResponse Success="true" Message="Successfully retrieved deep view of servers" StatusCode="0"&gt;

  &lt;AccountServers&gt;

    &lt;AccountServerGroup AccountAlias="ACT1"&gt;

      &lt;Servers&gt;

        &lt;Server

          ID="1000"

          HardwareGroupID="1197"

          Location="WA1"

          Name="SERVERDEMO01"

          Description="Server1"

          DnsName=""

          IsTemplate="false"

          Cpu="1"

          MemoryGB="2"

          DiskCount="1"

          TotalDiskSpaceGB="24"

          Status="UnderConstruction"

          PowerState="Stopped"

          InMaintenanceMode="false"

          IPAddress=""

          ServerType="1"

          ServiceLevel="2"

          OperatingSystem="18"

          DateModified="2012-09-13T16:03:42.943"

          ModifiedBy="user@tier3.com"&gt;

          &lt;IPAddresses  Address="142.25.114.13"  AddressType="RIP" /&gt;

        &lt;/Server&gt;

        &lt;Server

          ID="1001"

          HardwareGroupID="1111"

          Location="WA1"

          Name="SERVERDEMO02"

          Description="Server 2"

          IsTemplate="false"

          Cpu="0"

          MemoryGB="0"

          DiskCount="0"

          TotalDiskSpaceGB="0"

          Status="Deleted"

          PowerState="Stopped"

          InMaintenanceMode="false"

          ServerType="1"

          ServiceLevel="2"

          OperatingSystem="5"

          DateModified="2012-12-13T16:56:55.983"

          ModifiedBy="user@tier3.com" /&gt;

      &lt;/Servers&gt;

    &lt;/AccountServerGroup&gt;

    &lt;AccountServerGroup AccountAlias="ACT2"&gt;

      &lt;Servers&gt;

        &lt;Server

          ID="1003"

          HardwareGroupID="1595"

          Location="WA1"

          Name="SERVERDEMO03"

          Description="Server 3"

          DnsName="SERVERDEMO03"

          IsTemplate="false"

          Cpu="1"

          MemoryGB="1"

          DiskCount="3"

          TotalDiskSpaceGB="17"

          Status="Active"

          PowerState="Started"

          InMaintenanceMode="false"

          IPAddress="173.25.114.15"

          ServerType="1"

          ServiceLevel="2"

          OperatingSystem="20"

          DateModified="2013-06-28T20:34:12.953"

          ModifiedBy="user@tier3.com"&gt;

        &lt;/Server&gt;

      &lt;/Servers&gt;

    &lt;/AccountServerGroup&gt;

  &lt;/AccountServers&gt;

&lt;/GetAccountHierarchyServersResponse&gt;

</pre>

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