{{{
  "title": "Get Blueprints",
  "date": "9-26-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets a list of all Blueprints with the specified search criteria.

## URL

    REST:https://api.ctl.io/REST/Blueprint/GetBlueprints/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Blueprints.asmx?op=GetBlueprintsResponseMsg

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| CompanySize | Int | The target company size the of the Blueprint<br/>1 = 1 - 100<br/>2 = 101 - 1,000<br/>3 = 1,001 - 5,000<br/>4 =  5,000+ | No |
| OperatingSystems | Int [] | A list of the operating systems that a Blueprint contains<br/>Cent OS - 64 bit = 7<br/>Ubuntu - 64 bit = 20<br/>Debian 64-bit = 21<br />RedHat Enterprise Linux 64-bit = 22 <br/> RedHat Enterprise Linux 5 64-bit = 25<br/>Windows 2012 Datacenter 64-bit = 27<br/>Windows 2012 R2 Datacenter 64-bit = 28<br/>Ubuntu 12 64-Bit = 31<br/>CentOS 5 64-Bit = 33<br/> CentOS 6 64-Bit = 35<br/> Debian 6 64-Bit = 36 <br/>Debian 7 64-Bit = 37<br/>RedHat 6  64-Bit = 38<br/>CoreOS = 39<br/>PXE Boot = 40<br/>Ubuntu 14 64-Bit = 41<br/>RedHat 7 64-Bit = 42<br/>Windows 2008 R2 Standard 64-Bit = 43<br/>Windows 2008 R2 Enterprise 64-Bit = 44<br/>Windows 2008 R2 Datacenter 64-Bit = 45 |  No |
| Search | String | A keyword search within the Name and Description of the Blueprint | No |
| Visibility | Int | The visibility level of the Blueprint.<br/>1 = Public<br/>2 = Private<br/>3 = Private Shared | Yes |

### Examples

#### JSON

    {
      "CompanySize": "2",
      "OperatingSystems": [ 7, 20, 22, 28],
      "Search": "High Performance",
      "Visibility": 1
    }

#### XML

    <GetBlueprintsRequest>
          <CompanySize>2</CompanySize>
          <OperatingSystems>
              <OS>7</OS>
              <OS>20</OS>
              <OS>22</OS>
              <OS>28</OS>
          </OperatingSystems>
          <Search>High Performance</Search>
          <Visibility>1</Visibility>
    </GetBlueprintsRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Blueprints | Complex (see below) | A list of Blueprints (see below). |

### Blueprint Attributes

| Name | Type | Description |
| --- | --- | --- |
| ID | Int | The ID of the Blueprint. |
| Name | String | The name of the Blueprint. |

### Examples

#### JSON

    {
      "Blueprints":[
        {"ID":1,"Name":"Blueprint 01"},
        {"ID":2,"Name":"Blueprint 02"},
      ],
      "Success":true,
      "Message":"Success",
      "StatusCode":0
    }

#### XML

    <GetBlueprintsResponse Success="true" Message="Success" StatusCode="0">
        <Blueprints>
            <Blueprint ID="1" Name="Blueprint 01" />
            <Blueprint ID="2" Name="Blueprint 02" />
        </Blueprints>
    </GetBlueprintsResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 1201 | The Visibility value is missing or invalid. |
