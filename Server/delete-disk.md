{{{
  "title": "Delete Disk",
  "date": "11-28-2014",
  "author": "Brent Heinz",
  "attachments": []
}}}

Deletes a disk on a Server.

## URL

    REST: https://api.ctl.io/REST/Server/DeleteDisk/<format>
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=DeleteDisk

## Request

### Attributes

<table>
    <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Req.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the server. &nbsp;</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ScsiBusID</td>
      <td>String</td>
      <td>The SCSI bus ID of the disk.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ScsiDeviceID</td>
      <td>String</td>
      <td>The SCSI device ID of the disk.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>OverrideFailsafes</td>
      <td>Boolean</td>
      <td>Set to 'True' to override safety checks that prevent deleting typical primary operating system drives. e.g. SCSI Bus ID 0, SCSI Device ID 0 on Windows (typically C drive) and SCSI Bus ID 0, SCSI Device IDs 0,1,2 on Linux (typically boot, swap and
        root disks).</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

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

<table>
  <thead>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
    <tr>
      <td>Success</td>
      <td>Boolean</td>
      <td>True if the request was successful, otherwise False.</td>
    </tr>
    <tr>
      <td>Message</td>
      <td>String</td>
      <td>A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result.</td>
    </tr>
    <tr>
      <td>StatusCode</td>
      <td>Int</td>
      <td>This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state.</td>
    </tr>
    <tr>
      <td>RequestID</td>
      <td>Int</td>
      <td>The ID of the Queued request.Status of the request can be obtained by calling the&nbsp;<a href="../Blueprint/get-deployment-status.md">Get Deployment Status</a>&nbsp;method.</td>
    </tr>
  </tbody>
</table>

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

<table>
    <thead>
  <tr>
    <th>Status Code</th>
    <th>Description</th>
  </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;A Hardware Group with the specified ID cannot be found.
        <br />- OR -
        <br />A Server with the specified Name cannot be found&nbsp;</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Invalid Operation. &nbsp;Server must not have snapshots.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1410</td>
      <td>Name Required.</td>
    </tr>
    <tr>
      <td>1415</td>
      <td>Unknown snapshot state.</td>
    </tr>
  </tbody>
</table>