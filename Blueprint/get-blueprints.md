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
| OperatingSystems | Int[] | A list of the operating systems that a Blueprint contains<br/>Cent OS - 32 bit = 6<br/>Cent OS - 64 bit = 7<br/>Debian - 64 bit = 21<br/>Free BSD - 32 bit = 13<br/>Free BSD - 64 bit = 14<br/>Ubuntu - 32 bit = 19<br/>Ubuntu - 64 bit = 20<br/>Windows 2003 Enterprise - 32 bit = 15<br/>Windows2003 Enterprise - 64 bit = 16<br/>Windows 2003 - 32 bit = 2<br/>Windows 2003 - 64 bit = 3<br/>Windows 2008 - 32 bit = 4<br/>Windows 2008 - 64 bit = 5<br/>Windows 2008 Enterprise - 32 bit = 17<br/>Windows 2008 Enterprise - 64 bit = 18 |  No |
| Search | String | A keyword search within the Name and Description of the Blueprint | No |
| Visibility | Int | The visibility level of the Blueprint.<br/>1 = Public<br/>2 = Private<br/>3 = Private Shared | Yes |

### Examples

#### JSON

    {
      "CompanySize": "2",
      "OperatingSystems": [ 4, 5, 17, 18],
      "Search": "High Performance",
      "Visibility": 1
    }

#### XML

    <GetBlueprintsRequest>
          <CompanySize>2</CompanySize>
          <OperatingSystems>
              <OS>4</OS>
              <OS>5</OS>
              <OS>17</OS>
              <OS>18</OS>
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
