{{{
  "title": "Get Packages",
  "date": "11-24-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets a list of Blueprint Packages.

## URL

    REST: https://api.ctl.io/REST/Blueprint/GetPackages/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Blueprints.asmx?op=GetPackagesResponseMsg

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| Classification | Int | The type of Packages that should be returned.<br/>1 = System (reserved)<br/>2 = Script<br/>3 = Software</p> | Yes |
| Visibility | Int | The visibility of Packages that should be returned.<br/>1 = Public<br/>2 = Private<br/>3 = Shared | Yes |

### Examples

#### JSON

    { "Classification": "1", "Visibility": "1" }

#### XML

    <GetPackagesRequest>
      <Classification>1</Classification>
      <Visibility>1</Visibility>
    </GetPackagesRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Packages | Complex (see below) | A list of Packages (see below). |

### Package Attributes

| Name | Type | Description |
| --- | --- | --- |
| ID | Int | The ID of the Package.  This value is for reference only. |
| Name | String | The name of the Package. |
| Classification | Int | The classification of the Package.<br/>1 = System<br/>2 = Script<br/>3 = Software |

### Examples

#### JSON

    {
      "Packages": [
        {"ID":2,"Name":"Add Disk","Classification":1},
        {"ID":3,"Name":"Add IP Address","Classification":1},
        {"ID":4,"Name":"Add Mapped IP Address","Classification":1},
        {"ID":5,"Name":"Snapshot Server","Classification":1},
        {"ID":6,"Name":"Reboot Server","Classification":1}
      ],
      "Success":true,
      "Message":"Success",
      "StatusCode":0
    }

#### XML

    <GetPackagesResponse Success="true" Message="Success" StatusCode="0">
        <Packages>
            <Package ID="2" Name="Add Disk" Classification="1" />
            <Package ID="3" Name="Add IP Address" Classification="1" />
            <Package ID="4" Name="Add Mapped IP Address" Classification="1" />
            <Package ID="5" Name="Snapshot Server" Classification="1" />
            <Package ID="6" Name="Reboot Server" Classification="1" />
        </Packages>
    </GetPackagesResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 1200 | The Classification value is missing or invalid. |
| 1201 | The Visibility value is missing or invalid. |
