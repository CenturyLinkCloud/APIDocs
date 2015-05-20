{{{
  "title": "GetAllServersForAccountHierarchy",
  "date": "6-28-2013",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets a deep list of all servers for a given account hierarchy within a given data center. Use this operation to get a full list of all servers contained within an account and all its subaccounts.

## URL

    REST: https://api.ctl.io/REST/Server/GetAllServersForAccountHierarchy/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=GetAllServersForAccountHierarchyMsg

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that contains sub-accounts with servers. If not provided, it will assume the account to which the API user is mapped.  | No |
| Location | String | The data center location.  Otherwise leave blank and let it default to account's primary data center. | No |

### Examples

#### JSON

    {
      "AccountAlias": "ACCT",
      "Location": "WA1"
    }

#### XML

    <GetAllServersRequest>
        <AccountAlias>ACCT</AccountAlias>
        <Location>WA1</Location>
    </GetAllServersRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| AccountServers | Complex | A list of AccountServerGroups, each containing [Server Objects](../Server/server-object.md) |

### Examples

#### JSON

    {
      "AccountServers":[
        {
          "AccountAlias":"ACT1",
          "Servers":[
            {
              "ID":-1,
              "HardwareGroupID":1197,
              "HardwareGroupUUID":"8a03fbae8ddfe311b05f00505682315a",
              "Location":"WA1",
              "Name":"SERVERDEMO01",
              "Description":"Demo server",
              "DnsName":"",
              "IsTemplate":false,
              "IsHyperscale":false,
              "Cpu":1,
              "MemoryGB":2,
              "DiskCount":1,
              "TotalDiskSpaceGB":24,
              "Status":"UnderConstruction",
              "PowerState":"Stopped",
              "InMaintenanceMode":false,
              "IPAddress":"",
              "ServerType":1,
              "ServiceLevel":2,
              "OperatingSystem":18,
              "DateModified":"\/Date(1347577422943)\/",
              "ModifiedBy":"user@company.com",
              "IPAddresses":[
                {"Address":"142.25.114.13", "AddressType":"RIP"}
              ],
              "CustomFields":null
            }
          ]
        },
        {
          "AccountAlias":"ACT2",
          "Servers":[
            {
              "ID":-1,
              "HardwareGroupID":1595,
              "HardwareGroupUUID":"b9f454f2ae664998acc3302b24330c5b",
              "Location":"WA1",
              "Name":"SERVERDEMO03",
              "Description":"demo server",
              "DnsName":"QA1SSUBSERO9401",
              "IsTemplate":false,
              "IsHyperscale":false,
              "Cpu":1,
              "MemoryGB":1,
              "DiskCount":3,
              "TotalDiskSpaceGB":17,
              "Status":"Active",
              "PowerState":"Started",
              "InMaintenanceMode":false,
              "IPAddress":"173.25.114.15","ServerType":1,"ServiceLevel":2,"OperatingSystem":20,
              "DateModified":"\/Date(1372476852953)\/","ModifiedBy":"user@company.com",
              "IPAddresses":[
                {"Address":"173.25.114.15", "AddressType":"RIP"}
              ],
              "CustomFields":null
            }
          ]
        }
      ],
      "Success":true,
      "Message":"Successfully retrieved deep view of servers",
      "StatusCode":0
    }

#### XML

    <GetAccountHierarchyServersResponse Success="true" Message="Successfully retrieved deep view of servers" StatusCode="0">
      <AccountServers>
        <AccountServerGroup AccountAlias="ACT1">
          <Servers>
            <Server
              ID="-1"
              HardwareGroupID="1197"
              HardwareGroupUUID="8a03fbae8ddfe311b05f00505682315a"
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
              ModifiedBy="user@company.com">
              <IPAddresses  Address="142.25.114.13"  AddressType="RIP" />
            </Server>
          </Servers>
        </AccountServerGroup>
        <AccountServerGroup AccountAlias="ACT2">
          <Servers>
            <Server
              ID="-1"
              HardwareGroupID="1595"
              HardwareGroupUUID="b9f454f2ae664998acc3302b24330c5b"
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
              ModifiedBy="user@company.com">
            </Server>
          </Servers>
        </AccountServerGroup>
      </AccountServers>
    </GetAccountHierarchyServersResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A Group with the specified ID cannot be found. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
