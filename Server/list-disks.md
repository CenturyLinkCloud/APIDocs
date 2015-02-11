{{{
  "title": "ListDisks",
  "date": "11-28-2014",
  "author": "Luke Bakken",
  "attachments": []
}}}

Lists the disks on a Server.

## URL

    REST: https://api.tier3.com/REST/Server/ListDisks/<format>
    SOAP: https://api.tier3.com/SOAP/Server.asmx?op=ListDisks

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
      <td>QueryGuestDiskNames</td>
      <td>Boolean</td>
      <td>Set to 'True' to retrieve disk mount points / drive letters.</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "AccountAlias": "UNK",

      "Name": "WA1T3NWEB01",

      "QueryGuestDiskNames": true

    }

#### XML

    <ListDiskRequest>

        <AccountAlias>UNK</AccountAlias>

        <Name>WEB</Name>

        <QueryGuestDiskNames>true</QueryGuestDiskNames>

    </ListDiskRequest>

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
      <td>Disks</td>
      <td>DiskInfo</td>
      <td>List of the disks on the server.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "Server": "WA1MDAUBU04",

      "HasSnapshot": false,

      "Disks": [

        {

          "Name": "[0:0]",

          "ScsiBusID": "0",

          "ScsiDeviceID": "0",

          "SizeGB": 16

        }

      ],

      "Success": true,

      "Message": "OK",

      "StatusCode": 0

    }

#### XML

    <ListDiskResponse Success="true" Message="OK" StatusCode="0" Server="WA1MDAUBU04" HasSnapshot="false">

        <Disks>

            <DiskInfo Name="[0:0]" ScsiBusID="0" ScsiDeviceID="0" SizeGB="16"/>

        </Disks>

    </ListDiskResponse>

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
      <td>Invalid Operation. &nbsp;Server must be in an active state, and must not have snapshots.</td>
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