{{{
  "title": "GetAllServersByModifiedDates",
  "date": "12-26-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets a deep list of all modified Servers for a given Hardware Group and its sub groups, or all Servers for a given location. To get all servers that have changed since a certain date, only provide a BeginDate and omit the EndDate.

## URL

    REST: https://api.ctl.io/REST/Server/GetAllServersByModifiedDates/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=GetAllServersByModifiedDatesResponseMsg

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the servers. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to query a particular sub-account. | No |
| HardwareGroupID | Int | The ID of the Hardware Group, or 0 if providing Location. | No |
| Location | String | The data center location.  Otherwise leave blank and provide HardwareGroupID or let it default to account's primary data center. | No |
| BeginDate | DateTime | Beginning of date range for querying modified servers. Can be a partial DateTime (e.g. 2013-05-10) or a full DateTime (e.g. 2013:05-10T14:30:12). If date is missing, then the value equals today minus one day. | No |
| EndDate | DateTime | End of date range for querying modified servers. Can be a partial DateTime (e.g. 2013-05-10) or a full DateTime (e.g. 2013:05-10T14:30:12). If date is missing, then the value is set to the current date time.  | No |

### Examples

#### JSON

    {
      "AccountAlias": "ACCT",
      "Location": "WA1",
      "BeginDate": "2013-05-01",
      "EndDate": "2013-06-30"
    }

#### XML

    <GetAllServersRequest>
        <AccountAlias>ACCT</AccountAlias>
        <Location>WA1</Location>
        <BeginDate>2013-05-01</BeginDate>
        <EndDate>2013-06-30</EndDate>
    </GetAllServersRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Servers | Complex | A list of [Server Objects](server-object.md). |

### Examples

#### JSON

    {
      "Success":true,
      "Message":"Success",
      "StatusCode":0,
      "Servers":[
        {
          "ID":1001,
          "HardwareGroupID":1,
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
          "IPAddresses: [
            {"Address":"172.0.0.1", "AddressType":1}
          ],
          "CustomFields":[
            { "CustomFieldID": 100, "Name": "My Field", "Type": "Text", "Value": "A test"},
            { "CustomFieldID": 101, "Name": "My Field 2", "Type": "Option","Value": "2"},
            { "CustomFieldID": 102, "Name": "My Field 3", "Type": "Checkbox","Value": "true"}
          ]
        }
      ]
    }

#### XML

    <GetServersResponse Success="true" Message="Successfully retrieved servers" StatusCode="0">
        <Servers>
            <Server ID="1001" HardwareGroupID="1" Name="WA1T3NWEB01" Description="WA1T3NWEB01"
              DnsName="WA1T3NWEB01" IsTemplate="false" Cpu="2" MemoryGB="4" DiskCount="3"
              TotalDiskSpaceGB="116" Status="Active" ServerType="1" ServiceLevel="2"
              OperatingSystem="2" PowerState="Started" Location="WA1" IPAddress="172.0.0.1">
                <IPAddresses>
                    <IPAddress Address="172.0.0.1" AddressType="RIP" />
                </IPAddresse>
                <CustomFields CustomFieldID="100" Name="My Field" Type="Text" Value="Test Value" />
                <CustomFields CustomFieldID="101" Name="My 2nd Field" Type="Option" Value="Value 3" />
                <CustomFields CustomFieldID="102" Name="My 3rd Field" Type="Checkbox" Value="true" />
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
