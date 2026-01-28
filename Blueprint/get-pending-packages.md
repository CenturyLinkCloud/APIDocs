{{{
  "title": "Get Pending Packages",
  "date": "12-2-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets a list of Blueprint Packages that are pending publication.

This list contains all Packages that were uploaded to  via FTP or that were uploaded in the UI via HTTP.

## URL

    REST: https://api.ctl.io/REST/Blueprint/GetPendingPackages/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Blueprints.asmx?op=GetPendingPackages

## Request

### Attributes

None.

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Packages | Complex (see below) | A list of Packages (see below) |

### Package Attributes

| Name | Type | Description |
| --- | --- | --- |
| ID | Int | The ID of the Package.<br/>This value is for reference only and will always be 0. |
| Name | String | The name of the Package.<br/>This will be the name of the Package zip file that was uploaded. |
| Classification | Int | This value will always be 0 for pending packages |

### Examples

#### JSON

    {
      "Packages": [
        {"ID":0,"Name":"Script 01","Classification":0},
        {"ID":0,"Name":"Software 01","Classification":0}
      ],
      "Success":true,
      "Message":"Success",
      "StatusCode":0
    }

#### XML

    <GetPackagesResponse Success="true" Message="Success" StatusCode="0">
        <Packages>
            <Package ID="0" Name="Script 01" Classification="0" />
            <Package ID="0" Name="Software 01" Classification="0" />
        </Packages>
    </GetPackagesResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
