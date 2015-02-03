{{{
  "title": "Server Object",
  "date": "10-28-2014",
  "author": "Luke Bakken",
  "attachments": []
}}}

<h3>Server Attributes</h3>
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
      <td>The ID of the Server.</td>
    </tr>
    <tr>
      <td>HardwareGroupID</td>
      <td>Int</td>
      <td>The ID of the containing&nbsp;Group.</td>
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
    <tr>
      <td>DnsName</td>
      <td>String</td>
      <td>The DNS name of the Server.&nbsp;</td>
    </tr>
    <tr>
      <td>Cpu</td>
      <td>Int&nbsp;</td>
      <td>The number of processors configured on the Server.</td>
    </tr>
    <tr>
      <td>MemoryGB&nbsp;</td>
      <td>Int&nbsp;</td>
      <td>Total GB of RAM configured on the Server.</td>
    </tr>
    <tr>
      <td>DiskCount</td>
      <td>Int&nbsp;</td>
      <td>Total number of disks configured on the Server.&nbsp;</td>
    </tr>
    <tr>
      <td>TotalDiskSpaceGB</td>
      <td>Int&nbsp;</td>
      <td>Total space across all disk configured on the Server.</td>
    </tr>
    <tr>
      <td>IsTemplate&nbsp;</td>
      <td>Bool&nbsp;</td>
      <td>True if the Server is a template, else False.</td>
    </tr>
    <tr>
      <td>Status&nbsp;</td>
      <td>
        <ul>
          <li>Json:Int</li>
          <li>Xml:String&nbsp;</li>
        </ul>
      </td>
      <td>
        <ol>
          <li>Active</li>
          <li>Archived</li>
          <li>Deleted</li>
          <li>UnderConstruction</li>
          <li>QueuedForArchive</li>
          <li>QueuedForDelete</li>
          <li>QueuedForRestore</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td>ServerType</td>
      <td>Int</td>
      <td>The type of server
        <ol>
          <li>Standard</li>
          <li>Premium</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td>ServiceLevel</td>
      <td>Int</td>
      <td>The service level/performance for the underlying data store
        <ol>
          <li>Premium</li>
          <li>Standard</li>
        </ol>
      </td>
    </tr>
    <tr>
      <td>OperatingSystem</td>
      <td>Int</td>
      <td>
        <ul>
          <li>2 = Windows 2003 32-bit</li>
          <li>3 = Windows 2003 64-bit</li>
          <li>4&nbsp;= Windows 2008 32-bit</li>
          <li>5 = Windows 2008 64-bit</li>
          <li>6 = CentOS 32-bit</li>
          <li>7 = CentOS 64-bit</li>
          <li>13 = FreeBSD 32-bit</li>
          <li>14 = FreeBSD 64-bit</li>
          <li>15 = Windows 2003 Enterprise 32-bit</li>
          <li>16 = Windows 2003 Enterprise 64-bit</li>
          <li>17 = Windows 2008 Enterprise 32-bit</li>
          <li>18 = Windows 2008 Enterprise 64-bit</li>
          <li>19 = Ubuntu 32-bit</li>
          <li>20 = Ubuntu 64-bit</li>
          <li>21 = Debian 64-bit</li>
          <li>22 = RedHat Enterprise Linux 64-bit</li>
          <li>24 = Windows 2012 64-bit</li>
          <li>25 = RedHat Enterprise Linux 5 64-bit</li>
          <li>26 = Windows 2008 Datacenter 64-bit</li>
          <li>
            <p>27 = Windows 2012 Datacenter 64-bit</p>
          </li>
          <li>
            <p>28 = Windows 2012 R2 Datacenter 64-Bit</p>
          </li>
          <li>29 =&nbsp;Ubuntu 10 32-Bit</li>
          <li>30 =&nbsp;Ubuntu 10 64-Bit</li>
          <li>31 = Ubuntu 12 64-Bit</li>
          <li>32 = CentOS 5 32-Bit</li>
          <li>33 = CentOS 5 64-Bit</li>
          <li>34 = CentOS 6 32-Bit</li>
          <li>35 = CentOS 6 64-Bit</li>
          <li>36 = Debian 6 64-Bit</li>
          <li>37 = Debian 7 64-Bit</li>
          <li>38 = RedHat 6 64-Bit&nbsp;</li>
          <li>39 - CoreOS</li>
          <li>40 - PXE Boot</li>
          <li>41 - Ubuntu 14 64-Bit</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>PowerState</td>
      <td>
        <ul>
          <li>Json:Int</li>
          <li>Xml:String&nbsp;</li>
        </ul>
      </td>
      <td>The current power state of the Server.
        <ul>
          <li>0 Stopped</li>
          <li>1 Started</li>
          <li>2 Paused&nbsp;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>InMaintenanceMode</td>
      <td>Boolean</td>
      <td>Indicates if the Server is in Maintenance Mode.</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>Home datacenter of the Server.</td>
    </tr>
    <tr>
      <td>IPAddress</td>
      <td>String</td>
      <td>The primary IP address of the Server.</td>
    </tr>
    <tr>
      <td>IPAddresses</td>
      <td>Complex</td>
      <td>A list of all IP Addresses assigned to the server (see below)</td>
    </tr>
    <tr>
      <td>CustomFields</td>
      <td>Complex</td>
      <td>A list of Custom Fields associated to this server (see below)</td>
    </tr>
  </tbody>
</table>
<h3>IPAddress Attributes</h3>
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
      <td>Address</td>
      <td>String</td>
      <td>The IP Address</td>
    </tr>
    <tr>
      <td>AddressType</td>
      <td>Int</td>
      <td>The type of the IP Address
        <ol>
          <li>RIP - Real IP (internal IP configured on the VLAN)</li>
          <li>MIP - Mapped IP (external IP configured on the Firewall)</li>
          <li>VIP - Virtual IP (external IP configured on the Load Balancer)&nbsp;</li>
        </ol>
      </td>
    </tr>
  </tbody>
</table>
<h3>CustomField Attributes</h3>
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
      <td>CustomFieldID</td>
      <td>Int</td>
      <td>Identifier that is associated with the Account Custom Field (Call Account/GetCustomFields for a list of all custom fields set at the account level)</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>Name for the Custom Field</td>
    </tr>
    <tr>
      <td>Type</td>
      <td>String</td>
      <td>Type of custom field: "Text","Option" or "Checkbox".&nbsp;</td>
    </tr>
    <tr>
      <td>Value</td>
      <td>String</td>
      <td>For Text: Any value;&nbsp;For Option values, call Account/GetCustomFields to see possible values to pass in. Checkbox values should be "true" or "false".</td>
    </tr>
  </tbody>
</table>
<p>Examples</p>
<pre>{

  "Servers": [

    {

      "ID": 105421,

      "HardwareGroupID": 2158,

      "Location": "WA1",

      "Name": "WA1MDAS-STD01",

      "Description": "foo",

      "DnsName": null,

      "IsTemplate": false,

      "Cpu": 0,

      "MemoryGB": 0,

      "DiskCount": 0,

      "TotalDiskSpaceGB": 0,

      "Status": "Archived",

      "PowerState": "Stopped",

      "InMaintenanceMode": false,

      "IPAddress": null,

      "ServerType": 1,

      "ServiceLevel": 2,

      "OperatingSystem": 20,

      "DateModified": "\/Date(1358410186310)\/",

      "ModifiedBy": "Tier3 System",

      "IPAddresses": [

        

      ],<br />      "CustomFields": []

    },

    {

      "ID": 105191,

      "HardwareGroupID": 5199,

      "Location": "WA1",

      "Name": "WA1MDA2K1202",

      "Description": "2k12",

      "DnsName": "WA1MDA2K1202",

      "IsTemplate": false,

      "Cpu": 1,

      "MemoryGB": 1,

      "DiskCount": 3,

      "TotalDiskSpaceGB": 110,

      "Status": "Active",

      "PowerState": "Stopped",

      "InMaintenanceMode": false,

      "IPAddress": "10.81.14.18",

      "ServerType": 1,

      "ServiceLevel": 2,

      "OperatingSystem": 24,

      "DateModified": "\/Date(1358793254250)\/",

      "ModifiedBy": "bob@tier3.com",

      "IPAddresses": [

        

      ],<br />      "CustomFields": []

    }

  ]

}</pre>