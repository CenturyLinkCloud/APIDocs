{{{
  "title": "ServerTemplateObject",
  "date": "6-11-2013",
  "author": "Luke Bakken",
  "attachments": []
}}}

### Server Template Object

| Name | Type | Description |
| --- | --- | --- |
| ID | Int | The ID of the Template. |
| Name | String | The name of the Template. |
| Description | String | The description of the Template. |
| Location | String | Home datacenter of the Template. |
| Cpu | Int | The number of processors configured in the Template. |
| MemoryGB | Int | Total GB of RAM configured in the Template. |
| DiskCount | Int | Total number of disks configured on the Template. |
| TotalDiskSpaceGB | Int | Storage space taken up by the Template. |
| OperatingSystem | Int | Operating System of the Template (see below). |

### Operating Systems

| Operating System | Description |
| --- | --- |
| 2 | Windows 2003 32-bit |
| 3 | Windows 2003 64-bit |
| 4 | Windows 2008 32-bit |
| 5 | Windows 2008 64-bit |
| 6 | CentOS 32-bit |
| 7 | CentOS 64-bit |
| 8 | Windows XP 32-bit |
| 9 | Windows Vista 32-bit |
| 10 | Windows Vista 64-bit |
| 11 | Windows 7 32-bit |
| 12 | Windows 7 64-bit |
| 13 | FreeBSD 32-bit |
| 14 | FreeBSD 64-bit |
| 15 | Windows 2003 Enterprise 32-bit |
| 16 | Windows 2003 Enterprise 64-bit |
| 17 | Windows 2008 Enterprise 32-bit |
| 18 | Windows 2008 Enterprise 64-bit |
| 19 | Ubuntu 32-bit |
| 20 | Ubuntu 64-bit |
| 21 | Debian 64-bit |
| 22 | RedHat Enterprise Linux 64-bit |
| 23 | Windows 8 64-bit |
| 24 | Windows 2012 64-bit |
| 25 | RedHat Enterprise Linux 5 64-bit |
| 26 | Windows 2008 Datacenter 64-bit |
| 27 | Windows 2012 Datacenter 64-bit |


### Examples

#### JSON

    {
      "RequestID:1,
      "Success":true,
      "Message":"Success",
      "StatusCode":0,
      "Templates":[
        {
          "ID":1001,
          "Name":"CENTOS-6-32",
          "Description":"Cent OS 6 | 32-bit",
          "Cpu":1,
          "MemoryGB":2,
          "DiskCount":1,
          "TotalDiskSpaceGB":8,
          "OperatingSystem":6
        },
        {
          "ID":1002,
          "Name":"WIN2008R2STD-64",
          "Description":"Windows 2008 R2 Standard | 64-bit",
          "Cpu":1,
          "MemoryGB":4,
          "DiskCount":1,
          "TotalDiskSpaceGB":16,
          "OperatingSystem":18
        }
      ]
    }

#### XML

    <GetTemplatesResponse Success="true" Message="Successfully retrieved templates" StatusCode="0">
        <Templates>
            <Template ID="1001" Name="CENTOS-6-32" Description="CentOS 6 | 32-bit" Cpu="1"
              MemoryGB="2" DiskCount="1" TotalDiskSpaceGB="8" OperatingSystem="6" />
            <Template ID="1001" Name="WIN2008R2STD-64" Description="Windows 2008 R2 Standard | 64-bit"
              Cpu="1" MemoryGB="4" DiskCount="1" TotalDiskSpaceGB="16" OperatingSystem="18" />
        </Templates>
    </GetTemplatesResponse>
