{{{
  "title": "AddPublicIPAddress",
  "date": "2-6-2014",
  "author": "Peter Kowalczyk",
  "attachments": []
}}}

Maps a public IP Address to a Server.

## URL

    REST: https://api.ctl.io/REST/Network/AddPublicIPAddress/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Network.asmx?op=AddPublicIPAddress

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts. | No |
| ServerName | String | The name of the server.   | Yes |
| IPAddress | String | An existing internal IP Address on the server to use for the mapping. Leaving this blank will assign a new internal IP Address. | No |
| ServerPassword | String | The existing password, for authentication. Required only if existing internal IP was not provided and new IP must be assigned. | Depends |
| AllowHTTP | Boolean | The public IP mapping will allow HTTP requests. | No |
| AllowHTTPonPort8080 | Boolean | The public IP mapping will allow HTTP requests on port 8080. | No |
| AllowHTTPS | Boolean | The public IP mapping will allow HTTPS requests. | No |
| AllowFTP | Boolean | The public IP mapping will allow FTP requests. | No |
| AllowFTPS | Boolean | The public IP mapping will allow FTPS requests. | No |
| AllowSFTP | Boolean | The public IP mapping will allow SFTP requests. | No |
| AllowSSH | Boolean | The public IP mapping will allow SSH requests. | No |
| AllowRDP | Boolean | The public IP mapping will allow RDP requests. | No |

### Examples

#### JSON

    {
      "AccountAlias": "SUB1",
      "ServerName": "WA1T3NWEB01",
      "IPAddress": "1.1.1.1",
      "ServerPassword": "password",
      "AllowHTTP": true,
      "AllowHTTPonPort8080": false,
      "AllowHTTPS": false,
      "AllowFTP": false,
      "AllowFTPS": false,
      "AllowSFTP": false,
      "AllowSSH": false,
      "AllowRDP": false
    }

#### XML

    <AddIPAddressRequest>
        <AccountAlias>SUB1</AccountAlias>
        <ServerName>WA1T3NWEB01</ServerName>
        <IPAddress>1.1.1.1</IPAddress>
        <ServerPassword>password</ServerPassword>
        <AllowHTTP>true</AllowHTTP>
        <AllowHTTPonPort8080>false</AllowHTTPonPort8080>
        <AllowHTTPS>false</AllowHTTPS>
        <AllowFTP>false</AllowFTP>
        <AllowFTPS>false</AllowFTPS>
        <AllowSFTP>false</AllowSFTP>
        <AllowSSH>false</AllowSSH>
        <AllowRDP>false</AllowRDP>
    </AddIPAddressRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| RequestID | Int | The ID of the Blueprint Request submitted to perform this operation. You can check the status of this operation by calling the [GetRequestStatus](../Queue/get-request-status.md) method on the Queue API. |

### Examples

#### JSON

    {
     "Success":true,
     "Message":"Success",
     "StatusCode":0,
     "RequestID":1
    }

#### XML

    <QueuedItemResponse Success="true" Message="Success" StatusCode="0" RequestID="1" />

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A Server with the specified Name cannot be found.  |
| 6 | Invalid Operation.  Server must be in an active state. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 101 | Access Denied - Your API user account does not have access to the account specified. |
| 506 | Server Name Required. |
| 514 | Server Password Required. |
| 1000 | The IP Address provided is not configured on the Server. |
