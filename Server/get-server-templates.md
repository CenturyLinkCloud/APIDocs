{{{
  "title": "GetServerTemplates",
  "date": "8-20-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the list of Templates available to the account.

## URL

    REST: https://api.ctl.io/REST/Server/GetServerTemplates/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=GetServerTemplates

## Request

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Templates | Complex | A list of [Server Template Objects](server-template-object.md) |

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

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
