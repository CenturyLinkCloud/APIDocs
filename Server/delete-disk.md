{{{
  "title": "Delete Disk",
  "date": "11-28-2014",
  "author": "Brent Heinz",
  "attachments": []
}}}

Deletes a disk on a Server.

<div class="alert alert-warning">
<h2>V2 API Available</h2>
There is an equivalent V2 API that should be used instead. Please use the Servers | <a href="../v2/#servers-set-server-disks">Set Server Disks</a> API.
</div>

## URL

    REST: https://api.ctl.io/REST/Server/DeleteDisk/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=DeleteDisk

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts. | No |
| Name | String | The name of the server.   | Yes |
| ScsiBusID | String | The SCSI bus ID of the disk. | Yes |
| ScsiDeviceID | String | The SCSI device ID of the disk. | Yes |
| OverrideFailsafes | Boolean | Set to 'True' to override safety checks that prevent deleting typical primary operating system drives. e.g. SCSI Bus ID 0, SCSI Device ID 0 on Windows (typically C drive) and SCSI Bus ID 0, SCSI Device IDs 0,1,2 on Linux (typically boot, swap and root disks). | No |

### Examples

####

    {
      "AccountAlias": "UNK",
      "Name": "WA1UNKWEB01",
      "ScsiBusID": "0",
      "ScsiDeviceID": "1",
      "OverrideFailsafes": false
    }

#### XML

    <DeleteDiskRequest>
        <AccountAlias>UNK</AccountAlias>
        <Name>WA1UNKWEB01</Name>
        <ScsiBusID>0</ScsiBusID>
        <ScsiDeviceID>1</ScsiDeviceID>
        <OverrideFailsafes>false</OverrideFailsafes>
    </DeleteDiskRequest>

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
| 5 | Resource Not Found.  A Hardware Group with the specified ID cannot be found. - OR - A Server with the specified Name cannot be found  |
| 6 | Invalid Operation.  Server must not have snapshots. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 1410 | Name Required. |
| 1415 | Unknown snapshot state. |
