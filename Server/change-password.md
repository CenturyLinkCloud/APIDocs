{{{
  "title": "Change Password",
  "date": "5-1-2013",
  "author": "Peter Kowalczyk",
  "attachments": []
}}}

Updates the Admin/Root password for a Server.

### URL

    REST: https://api.ctl.io/REST/Server/ChangePassword/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=ChangePassword

## Request


### Attributes
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts. | No |
| Name | String | The name of the server.   | Yes |
| CurrentPassword | String | The existing password, for authentication. | Yes |
| NewPassword | String | The new password to apply. | Yes |

### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "Name": "WA1T3NWEB01",
      "CurrentPassword": "password",
      "NewPassword": "newPassword"
    }

#### XML

    <ChangePasswordRequest>
        <AccountAlias>UNK</AccountAlias>
        <Name>QA1FMACC554L01</Name>
        <CurrentPassword>password</CurrentPassword>
        <NewPassword>newPassword</NewPassword>
    </ChangePasswordRequest>

## Response

### Attributes

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

    <APIResponse Success="true" Message="Success" StatusCode="0" />

### Status Codes
| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A Server with the specified Name cannot be found.  |
| 6 | Invalid Operation.  Server must be in an active state. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 1410 | Name Required. |
| 1411 | Password Required.  Both current and new passwords are required. |
