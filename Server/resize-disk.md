{{{
  "title": "ResizeDisk",
  "date": "5-1-2013",
  "author": "Luke Bakken",
  "attachments": []
}}}

Resizes a disk on a Server.

## URL

    REST: https://api.ctl.io/REST/Server/ResizeDisk/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=ResizeDisk

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts. | No |
| Name | String | The name of the server.   | Yes |
| ScsiBusID | String | The SCSI bus ID of the disk. | Yes |
| ScsiDeviceID | String | The SCSI device ID of the disk. | Yes |
| ResizeGuestDisk | Boolean | Set to 'True' to attempt to expand the file system on the disk after the resize. | No |
| NewSizeGB | Int | The expanded size of the disk. Must be greater than the existing disk size. | Yes |

### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "Name": "WA1T3NWEB01",
      "ScsiBusID": "0",
      "ScsiDeviceID": "2",
      "ResizeGuestDisk": true,
      "NewSizeGB": 50
    }

#### XML

    <ResizeDiskRequest>
        <AccountAlias>UNK</AccountAlias>
        <Name>WEB</Name>
        <ScsiBusID>0</ScsiBusID>
        <ScsiDeviceID>2</ScsiDeviceID>
        <ResizeGuestDisk>true</ResizeGuestDisk>
        <NewSizeGB>50</NewSizeGB>
    </ResizeDiskRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| RequestID | Int | The ID of the Queued request.Status of the request can be obtained by calling the [Get Deployment Status](../Blueprint/get-deployment-status.md) method. |

### Examples

#### JSON

    {
      "RequestID":1,
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
| 5 | Resource Not Found.  A Hardware Group with the specified ID cannot be found. - OR - A Server with the specified Name cannot be found |
| 6 | Invalid Operation.  Server must be in an active state, and must not have snapshots. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 1410 | Name Required. |
| 1415 | Unknown snapshot state. |
