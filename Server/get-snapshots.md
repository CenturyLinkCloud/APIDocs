{{{
  "title": "GetSnapshots",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the list of Snapshots associated with the server.

<div class="alert alert-warning">
<h2>V2 API Available</h2>
There is an equivalent V2 API that should be used instead. Please use the Servers | <a href="../v2/#servers-get-server">Get Server</a> API.
</div>

## URL

    REST: https://api.ctl.io/REST/Server/GetSnapshots/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=GetSnapshots

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access servers in your sub accounts | No |
| Name | String | The name of the Server to get Snapshots for. | Yes |

### Examples

#### JSON

    {
      "Name": "DEMOFIRST01",
      "AccountAlias": "UNK"
    }

#### XML

    <ServerRequest>
        <AccountAlias>ACCT</AccountAlias>
        <Name>SERVER01</Name>
    </ServerRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Snapshots | Complex (see below) | A list of Snapshots (see below). |

### Snapshot Attributes

| Name | Type | Description |
| --- | --- | --- |
| Name | String | The full name of the Snapshot. |
| Description | String | The description of the Snapshot. |
| DateCreated | DateTime | The time (in UTC) when the Snapshot was created. |

### Examples

#### JSON

    {
      "RequestID:1,
      "Success":true,
      "Message":"Success",
      "StatusCode":0,
      "Snapshots":[
        {"Name":"2012-01-01-12:00:00","Description":"Snapshot (2012-01-01-12:00:00)","DateCreated":"\/Date(1330047404893)\/"}
      ]
    }

#### XML

    <GetSnapshotsResponse Success="true" Message="Successfully retrieved snapshots" StatusCode="0">
        <Snapshots>
            <Snapshot>
                <Name>2012-01-01-12:00:00</Name>
                <Description>Snapshot (2012-01-01-12:00:00)</Description>
                <DateCreated>2012-01-01T12:00:00.000</DateCreated>
            </Snapshot>
        </Snapshots>
    </GetSnapshotsResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 5 | Resource Not Found.  A server with the specified name could not be found. |
| 6 | Invalid Operation.  Server must be in an active state. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1410 | Name is required. |
