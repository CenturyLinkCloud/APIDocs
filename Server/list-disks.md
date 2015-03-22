{{{
  "title": "ListDisks",
  "date": "11-28-2014",
  "author": "Luke Bakken",
  "attachments": []
}}}

Lists the disks on a Server.

## URL

    REST: https://api.ctl.io/REST/Server/ListDisks/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=ListDisks

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts. | No |
| Name | String | The name of the server. | Yes |
| QueryGuestDiskNames | Boolean | Set to 'True' to retrieve disk mount points / drive letters. | No |

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

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Disks | DiskInfo | List of the disks on the server. |

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
