{{{
  "title": "DeleteUser",
  "date": "11-20-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Delete a user associated with a given account. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/User/DeleteUser/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/User.asmx?op=DeleteUser

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| UserName | String | User name, which is typically the email address. | Yes |

### Examples

#### JSON

    {
      "UserName": "user3@company.com"
    }

#### XML (REST)

    <UserRequest>
        <UserName>user3@company.com</UserName>
    </UserRequest>

#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema"
      xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
        <soap12:Body>
            <DeleteUser xmlns="http://www.tier3.com/">
                <request>
                    <UserName>user3@company.com</UserName>
                </request>
            </DeleteUser>
        </soap12:Body>
    </soap12:Envelope>

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
      "Message":"User deleted.",
      "StatusCode":0
    }

#### XML (REST)

    <APIResponse Success="true" Message="User deleted." StatusCode="0" />

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema">
        <soap:Body>
            <DeleteUserResponse xmlns="http://www.tier3.com/">
                <DeleteUserResult Success="true" Message="User deleted." StatusCode="0"/>
            </DeleteUserResponse>
        </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1704 | Username Required.  You must provide a valid user name when calling this method. |
| 1705 | User Not Found.  Provided user name does not exist. |
