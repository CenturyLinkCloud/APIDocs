{{{
  "title": "GetArchiveServers",
  "date": "2-28-2012",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the list of Archive Servers.

## URL

    REST: https://api.ctl.io/REST/Server/GetArchiveServers/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=GetArchiveServers

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Servers | Complex (see below) | A list of Archive Servers (see below) |

### Archive Server Attributes

| Name | Type | Description |
| --- | --- | --- |
| ID | Int | The ID of the Server.<br/>_Deprecated. Value is -1._ |
| Name | String | The full name of the Server. |
| Description | String | The description of the Server as provided on creation. |

### Examples

#### JSON

    {
      "Success":true,
      "Message":"Success",
      "StatusCode":0,
      "Servers": [
        {"ID":-1, "Name":"WA1T3NWEB01", "Description":"WA1T3NWEB01"},
        {"ID":-1, "Name":"WA1T3NWEB02", "Description":"WA1T3NWEB02"}
       ]
    }

#### XML

    <GetServersResponse Success="true" Message="Successfully retrieved servers" StatusCode="0">
        <Servers>
            <Server ID="-1" Name="WA1T3NWEB01" Description="WA1T3NWEB01"/>
            <Server ID="-1" Name="WA1T3NWEB02" Description="WA1T3NWEB02"/>
        </Servers>
    </GetServersResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  The archive group could not be found.  Please contact support. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
