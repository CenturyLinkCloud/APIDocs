{{{
  "title": "Delete Snapshot",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Deletes a named snapshot for a specified server.

## URL

    REST: https://api.ctl.io/REST/Server/DeleteSnapshot/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=DeleteSnapshot

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access servers in your sub accounts | No |
| Name | String | The name of the Server. | Yes |
| SnapshotName | String | The name of the Snapshot to delete | Yes |

### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "Name": "1",
      "SnapshotName": "2012-01-01-12:00:00"
    }

#### XML

    <SnapshotRequest>
        <AccountAlias>ACCT</AccountAlias>
        <Name>SERVER01</Name>
        <SnapshotName>2012-01-01-12:00:00</SnapshotName>
    </SnapshotRequest>

## Response

### Attribute

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |

### Examples

#### JSON

    {
      "Success":true,
      "Message":"Success",
      "StatusCode":0
    }

#### XML

    <APIResponse Success="true" Message="Success" StatusCode="0"/>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found. A Server with the specified name cannot be found. -OR- A Snapshot with the specified name cannot be found. |
| 6 | Invalid Operation.  Server must be in an active state. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1410 | Name required.  The name parameter must be specified. |
| 1412 | SnapshotName required.  The name of the snapshot must be specified. |
