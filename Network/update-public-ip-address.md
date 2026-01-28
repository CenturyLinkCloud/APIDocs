{{{
  "title": "UpdatePublicIPAddress",
  "date": "5-1-2013",
  "author": "Peter Kowalczyk",
  "attachments": []
}}}

Configures firewall settings on a public IP Address.

<div class="alert alert-warning">
<h2>V2 API Available</h2>
There is an equivalent V2 API that should be used instead. Please use the Public IP | <a href="../v2/#public-ip-update-public-ip-address">Update Public IP Address</a> API.
</div>

## URL

    REST: https://api.ctl.io/REST/Network/UpdatePublicIPAddress/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Network.asmx?op=UpdatePublicIPAddress

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server.  If not provided it will assume the Account the API user is mapped to.  Providing this value gives you the ability to manage servers in your sub accounts. | No |
| ServerName | String | The name of the server.   | Yes |
| PublicIPAddress | String | The public, mapped IP to manage. | Yes |
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
      "PublicIPAddress": "1.1.1.1",
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

    <UpdateIPAddressRequest>
        <AccountAlias>SUB1</AccountAlias>
        <ServerName>WA1T3NWEB01</ServerName>
        <PublicIPAddress>1.1.1.1</PublicIPAddress>
        <AllowHTTP>true</AllowHTTP>
        <AllowHTTPonPort8080>false</AllowHTTPonPort8080>
        <AllowHTTPS>false</AllowHTTPS>
        <AllowFTP>false</AllowFTP>
        <AllowFTPS>false</AllowFTPS>
        <AllowSFTP>false</AllowSFTP>
        <AllowSSH>false</AllowSSH>
        <AllowRDP>false</AllowRDP>
    </UpdateIPAddressRequest>

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
      "Success": true,
      "Message": "Success",
      "StatusCode": 0,
      "RequestID": 1
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
| 101 | Access Denied - Your API user does not have access to the account specified. |
| 506 | Server Name Required. |
| 1511 | Public IP Address Required. |
| 1000 | The Public IP Address provided is not configured on the Server. |
