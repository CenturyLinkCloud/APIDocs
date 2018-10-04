{{{
  "title": "GetAllServers",
  "date": "6-21-2013",
  "author": "Peter Kowalczyk",
  "attachments": []
}}}

Gets a deep list of all Servers for a given Hardware Group and its sub groups, or all Servers for a given location.

## URL

    REST: https://api.ctl.io/REST/Server/GetAllServers/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=GetAllServersResponseMsg

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the servers. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access servers in your sub accounts. | No |
| HardwareGroupUUID | String | The unique identifier of the Hardware Group, or empty string if providing Location. | No |
| Location | String | The data center location.  Otherwise leave blank and provide HardwareGroupUUID. | No |

### Examples

#### JSON

    {
      "AccountAlias":"ACCT",
      "HardwareGroupUUID": "8a03fbae8ddfe311b05f00505682315a",
      "Location": "WA1"
    }

#### XML

    <GetAllServersRequest>
        <AccountAlias>ACCT</AccountAlias>
        <HardwareGroupUUID>8a03fbae8ddfe311b05f00505682315a</HardwareGroupUUID>
        <Location>WA1</Location>
    </GetAllServersRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Servers | Complex | A list of [Server Objects](../Server/server-object.md) |

### Examples

#### JSON

    {
      "Success":true,
      "Message":"Success",
      "StatusCode":0,
      "Servers": [
        {
          "ID":-1,
          "HardwareGroupID":1,
          "HardwareGroupUUID":"8a03fbae8ddfe311b05f00505682315a",
          "Name":"WA1T3NWEB01",
          "Description":"WA1T3NWEB01",
          "DnsName":"WA1T3NWEB01",
          "IsTemplate":false,
          "Cpu":2,
          "MemoryGB":4,
          "DiskCount":3,
          "TotalDiskSpaceGB":116,
          "Status":"Active",
          "ServerType":"2",
          "ServiceLevel":"1",
          "OperatingSystem":4,
          "PowerState":"Started",
          "Location":"WA1",
          "IPAddress":"172.0.0.1"
          "IPAddresses:[
            {"Address":"172.0.0.1", "AddressType":1}
          ],
          "CustomFields":[
            { "ID":"9f4150b68d4340cca652a209a4b32c34", "CustomFieldID": -1, "Name": "My Field", "Type": "Text", "Value": "A test"},
            { "ID":"393a0aafd15d47118d57dde0a3d556e3", "CustomFieldID": -1, "Name": "My Field 2", "Type": "Option", "Value": "2"},
            { "ID":"7997a9c0181644c99e490c5c465cf297", "CustomFieldID": -1, "Name": "My Field 3", "Type": "Checkbox", "Value": "true"}
          ]
        },
        {
          "ID":-1,
          "HardwareGroupID":1,
          "HardwareGroupUUID":"8a03fbae8ddfe311b05f00505682315a",
          "Name":"WA1T3NWEB02",
          "Description":"WA1T3NWEB02",
          "DnsName":"WA1T3NWEB02",
          "IsTemplate":false,
          "Cpu":2,
          "MemoryGB":4,
          "DiskCount":3,
          "TotalDiskSpaceGB":116,
          "Status":"Active",
          "ServerType":"1",
          "ServiceLevel":"2",
          "OperatingSystem":6,
          "PowerState":"Started",
          "Location":"WA1",
          "IPAddress":"172.0.0.2",
          "IPAddresses: [
            {"Address":"172.0.0.2", "AddressType":1}
          ],
          "CustomFields": []
        }
      ]
    }

#### XML

    <GetServersResponse Success="true" Message="Successfully retrieved servers" StatusCode="0">
        <Servers>
            <Server ID="-1" HardwareGroupID="1" HardwareGroupUUID="8a03fbae8ddfe311b05f00505682315a"
              Name="WA1T3NWEB01" Description="WA1T3NWEB01" DnsName="WA1T3NWEB01"
              IsHyperscale="false" IsTemplate="false" Cpu="2" MemoryGB="4" DiskCount="3"
              TotalDiskSpaceGB="116" Status="Active" ServerType="1" ServiceLevel="2"
              OperatingSystem="2" PowerState="Started" Location="WA1" IPAddress="172.0.0.1">
                <IPAddresses>
                    <IPAddress Address="172.0.0.1" AddressType="RIP" />
                </IPAddresses>
                <CustomFields ID="9f4150b68d4340cca652a209a4b32c34" CustomFieldID="-1" Name="My Field" Type="Text" Value="Test Value" />
                <CustomFields ID="393a0aafd15d47118d57dde0a3d556e3" CustomFieldID="-1" Name="My 2nd Field" Type="Option" Value="Value 3" />
                <CustomFields ID="7997a9c0181644c99e490c5c465cf297" CustomFieldID="-1" Name="My 3rd Field" Type="Checkbox" Value="true" />
            </Server>
            <Server ID="-1" HardwareGroupID="1" HardwareGroupUUID="8a03fbae8ddfe311b05f00505682315a"
              Name="WA1T3NWEB02" Description="WA1T3NWEB02" DnsName="WA1T3NWEB02"
              IsHyperscale="false" IsTemplate="false" Cpu="2" MemoryGB="4" DiskCount="3"
              TotalDiskSpaceGB="116" Status="Active" ServerType="1" ServiceLevel="2"
              OperatingSystem="2" PowerState="Started" Location="WA1" IPAddress="172.0.0.2">
                <IPAddresses>
                    <IPAddress Address="172.0.0.2" AddressType="RIP"/>
                </IPAddresses>
                <CustomFields />
           </Server>
        </Servers>
    </GetServersResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A Group with the specified ID cannot be found. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
