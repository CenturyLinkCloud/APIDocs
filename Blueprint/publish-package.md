{{{
  "title": "Publish Package",
  "date": "12-2-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Publishes a Blueprint Package for use within the Blueprint Designer.

## URL

    REST: https://api.ctl.io/REST/Blueprint/PublishPackage/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Blueprints.asmx?op=PublishPackage

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| Classification | Int | The type of Packages that should be returned<br/>1 = System (reserved)<br/>2 = Script<br/>3 = Software | Yes |
| Name | String | The name of the Package file to publish.<br/>Obtained via the [GetPendingPackages](../Blueprints/get-pending-packages.md) method. | Yes |
| OperatingSystems | Int[] | A list of operating systems that this Package can be deployed to (see table below).<br/>* The most recent list is always available from the [ListAvailableServerTemplates](../Server/list-available-server-templates.md) API call. | Yes |
| Visibility | Int | The visibility of Packages that should be returned<br/>1 = Public<br/>2 = Private<br/>3 = Shared | Yes |

### Operating Systems

| Operating System | Description |
| --- | --- |
| 2  | Windows 2003 R2 Standard 32-bit |
| 3  | Windows 2003 R2 Standard 64-bit |
| 5  | Windows 2008 R2 Standard 64-bit |
| 15 | Windows 2003 R2 Enterprise 32-bit |
| 16 | Windows 2003 R2 Enterprise 64-bit |
| 18 | Windows 2008 R2 Enterprise 64-bit |
| 20 | BOSH Stemcell Template |
| 20 | Stemcell - Micro-BOSH |
| 25 | RedHat Enterprise Linux 5 64-bit |
| 26 | Windows 2008 R2 Datacenter Edition 64-bit |
| 27 | Windows 2012 Datacenter Edition 64-bit |
| 28 | Windows 2012 R2 Datacenter Edition 64-bit |
| 29 | Ubuntu 10 32-bit |
| 30 | Ubuntu 10 64-bit |
| 30 | Web Fabric Ubuntu x64 Template |
| 30 | Web Fabric Ubuntu x64 Template V2 |
| 31 | Ubuntu 12 64-bit |
| 32 | CentOS 5 32-bit |
| 33 | CentOS 5 64-bit |
| 34 | CentOS 6 32-bit |
| 35 | CentOS 6 64-bit |
| 36 | Debian 6 64-bit |
| 37 | Debian 7 64-bit |
| 38 | RedHat Enterprise Linux 6 64-bit |
| 40 | PXE Boot [EXPERIMENTAL] |
| 41 | Ubuntu 14 64-bit |

### Examples

#### JSON

    {
      "Classification": "2",
      "Name":"Script01.zip",
      "OperatingSystems":[4,5],
      "Visibility": "1"
    }

#### XML

    <PublishPackageRequest>
        <Classification>2</Classification>
        <Name>Script01.zip</Name>
        <OperatingSystems>
        <OS>4</OS>
        <OS>5</OS>
        </OperatingSystems>
        <Visibility>1</Visibility>
    </PublishPackageRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| RequestID | Int | The ID of the Queued request to publish the Package.<br/>Status of the request can be obtained by calling the [GetRequestStatus](../Queue/get-request-status.md) method. |

### Examples

#### JSON

    {
      "RequestID": 1,
      "Success":true,
      "Message":"Success",
      "StatusCode":0
    }

#### XML

    <QueuedItemResponse Success="true" Message="Success" StatusCode="0">
        <RequestID>1</RequestID>
    </QueuedItemResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 1200 | The Classification value is missing or invalid. |
| 1201 | The Visibility value is missing or invalid. |
| 1202 | The supplied operating system values are missing or invalid. |
