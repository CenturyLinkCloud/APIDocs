{{{
  "title": "ServerTemplateObject",
  "date": "6-11-2013",
  "author": "Luke Bakken",
  "attachments": []
}}}

<h3>Server Template Object</h3>
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
      <td>The ID of the Template.</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Template.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>The description of the&nbsp;Template.</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>Home datacenter of the Template.</td>
    </tr>
    <tr>
      <td>Cpu</td>
      <td>Int</td>
      <td>The number of processors configured in the Template.</td>
    </tr>
    <tr>
      <td>MemoryGB</td>
      <td>Int</td>
      <td>Total GB of RAM configured in the Template.</td>
    </tr>
    <tr>
      <td>DiskCount</td>
      <td>Int</td>
      <td>Total number of disks configured on the Template.</td>
    </tr>
    <tr>
      <td>TotalDiskSpaceGB</td>
      <td>Int</td>
      <td>Storage space taken up by the Template.</td>
    </tr>
    <tr>
      <td>OperatingSystem</td>
      <td>Int</td>
      <td>
        <ul>
          <li>2 = Windows 2003 32-bit</li>
          <li>3 = Windows 2003 64-bit</li>
          <li>4 = Windows 2008 32-bit</li>
          <li>5 = Windows 2008 64-bit</li>
          <li>6 = CentOS 32-bit</li>
          <li>7 = CentOS 64-bit</li>
          <li>8 = Windows XP 32-bit</li>
          <li>9 = Windows Vista 32-bit</li>
          <li>10 = Windows Vista 64-bit</li>
          <li>11 = Windows 7 32-bit</li>
          <li>12 = Windows 7 64-bit</li>
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
          <li>23 = Windows 8 64-bit</li>
          <li>24 = Windows 2012 64-bit</li>
          <li>25 = RedHat Enterprise Linux 5 64-bit</li>
          <li>26 = Windows 2008 Datacenter 64-bit</li>
          <li>27 = Windows 2012 Datacenter 64-bit</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
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