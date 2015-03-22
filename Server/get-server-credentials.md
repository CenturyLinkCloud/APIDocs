{{{
  "title": "GetServerCredentials",
  "date": "2-6-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the credentials for the specified server.

## URL

    REST: https://api.ctl.io/REST/Server/GetServerCredentials/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=GetServerCredentials

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access servers in your sub accounts. | No |
| Name | String | The Name of the server. | Yes |

### Examples

#### JSON

    {
      "AccountAlias": "ACCT",
      "Name": "DC1ACCTSVR01"
    }

#### XML

    <ServerRequest>
        <AccountAlias>ACCT</AccountAlias>
        <Name>DC1ACCTSVR01</Name>
    </ServerRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Username | String | The administrator or root user name for the server. |
| Password | String | The password associated with the account. |

### Examples

#### JSON

    {
        "Success":true,
        "Message":"Success",
        "StatusCode":0,
        "Username":"administrator",
        "Password":"password"
    }

#### XML

    <GetServerCredentialsResponse Success="true" Message="Successfully retrieved servers" StatusCode="0">
        <Username>administrator</Username>
        <Password>password</Password>
    </GetServerCredentialsResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A server with the specified name cannot be found. |
| 6 | Invalid Operation.  Server must be in an active state. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1410 | Server Name Required. |
