{{{
  "title": "Server Object",
  "date": "10-28-2014",
  "author": "Luke Bakken",
  "attachments": []
}}}

 ### Server Attributes
| Name | Type | Description |
| --- | --- | --- |
| ID | Int | The ID of the Server.<br/>_Deprecated. Value is -1._ |
| HardwareGroupID | Int | The legacy ID of the containing Group.<br/>_Deprecated. Not available after May 6, 2015. Use UUID instead._ |
| HardwareGroupUUID | String | The unique identifier of the containing Group. |
| Name | String | The full name of the Server. |
| Description | String | The description of the Server as provided on creation. |
| DnsName | String | The DNS name of the Server.  |
| Cpu | Int  | The number of processors configured on the Server. |
| MemoryGB  | Int  | Total GB of RAM configured on the Server. |
| DiskCount | Int  | Total number of disks configured on the Server.  |
| TotalDiskSpaceGB | Int  | Total space across all disk configured on the Server. |
| IsTemplate  | Bool  | True if the Server is a template, else False. |
| IsHyperscale  | Bool  | True if the Server is a Hyperscale instance, else False. |
| Status  | Json:Int / Xml:String | `Active`, `Archived`, `Deleted`, `UnderConstruction`, `QueuedForArchive`, `QueuedForDelete`, or `QueuedForRestore` |
| ServerType | String | The type of server. `Standard` or `Premium` |
| ServiceLevel | String | The service level/performance for the underlying data store.  `Standard` or `Premium` |
| OperatingSystem | Int | Operating System of the server (see below). |
| PowerState | Json:Int / Xml:String | The current power state of the Server.<br/>0 = Stopped<br/>1 = Started<br/>2 = Paused |
| InMaintenanceMode | Boolean | Indicates if the Server is in Maintenance Mode. |
| Location | String | Home datacenter of the Server. |
| IPAddress | String | The primary IP address of the Server. |
| IPAddresses | Complex | A list of all IP Addresses assigned to the server (see below) |
| CustomFields | Complex | A list of Custom Fields associated to this server (see below) |

### Operating Systems

| Operating System | Description |
| --- | --- |
| 7 | CentOS 64-bit |
| 20 | Ubuntu 64-bit |
| 21 | Debian 64-bit |
| 22 | RedHat Enterprise Linux 64-bit |
| 25 | RedHat Enterprise Linux 5 64-bit |
| 27 | Windows 2012 Datacenter 64-bit |
| 28 | Windows 2012 R2 Datacenter 64-Bit |
| 31 | Ubuntu 12 64-Bit |
| 33 | CentOS 5 64-Bit |
| 35 | CentOS 6 64-Bit |
| 36 | Debian 6 64-Bit |
| 37 | Debian 7 64-Bit |
| 38 | RedHat 6 64-Bit  |
| 39 | CoreOS |
| 40 | PXE Boot |
| 41 | Ubuntu 14 64-Bit |
| 42 | RedHat 7 64-Bit |
| 43 | Windows 2008 R2 Standard 64-Bit |
| 44 | Windows 2008 R2 Enterprise 64-Bit |
| 45 | Windows 2008 R2 Datacenter 64-Bit |
| 46 | Windows 2012 R2 Standard 64-bit |

### IPAddress Attributes

| Name | Type | Description |
| --- | --- | --- |
| Address | String | The IP Address |
| AddressType | Int | The type of the IP Address<br/>RIP - Real IP (internal IP configured on the VLAN)<br/>MIP - Mapped IP (external IP configured on the Firewall)<br/>VIP - Virtual IP (external IP configured on the Load Balancer) |

### CustomField Attributes

| Name | Type | Description |
| --- | --- | --- |
| ID | String | Unique identifier that is associated with the Account Custom Field. Call [Account/GetCustomFields](../Account/GetCustomFields.md) for a list of all custom fields set at the account level. |
| CustomFieldID | Int | _Deprecated. Value is -1. Use CustomFieldType instead._ |
| Name | String | Name for the Custom Field. |
| Type | String | Type of custom field: `Text`, `Option` or `Checkbox`.  |
| Value | String | For Text: Any value; For Option values, call [Account/GetCustomFields](../Account/GetCustomFields.md) to see possible values to pass in. Checkbox values should be "true" or "false". |

### Examples

#### JSON

    {
      "Servers": [
        {
          "ID": -1,
          "HardwareGroupID": 2158,
          "HardwareGroupUUID": "4c20467154cb4de99a381cc011a20b96"
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
          "OperatingSystem": 41,
          "DateModified": "\/Date(1358410186310)\/",
          "ModifiedBy": "CenturyLink Cloud System",
          "IPAddresses": [],
          "CustomFields": []
        },
        {
          "ID": -1,
          "HardwareGroupID": 5199,
          "HardwareGroupUUID": "ea97c6e09f604eb689dcdc080114b04d"
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
          "OperatingSystem": 28,
          "DateModified": "\/Date(1358793254250)\/",
          "ModifiedBy": "bob@company.com",
          "IPAddresses": [],
          "CustomFields": []
        }
      ]
    }
