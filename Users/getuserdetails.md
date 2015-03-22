{{{
  "title": "GetUserDetails",
  "date": "11-12-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the details of a specific user associated with a given account. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/User/GetUserDetails/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/User.asmx?op=GetUserDetails

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | Short code for a particular account. | Yes |
| UserName | String | User name, which is typically the email address. | Yes |

### Examples

#### JSON

    {
      "AccountAlias": "1000",
      "UserName": "user1@company.com"
    }

#### XML (REST)

    <GetUserRequest>
        <AccountAlias>RSDA</AccountAlias>
        <UserName>user1@company.com</UserName>
    </GetUserRequest>

#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema"
      xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
        <soap12:Body>
            <GetUserDetails xmlns="http://www.tier3.com/">
                <request>
                    <AccountAlias>1000</AccountAlias>
                    <UserName>user1@company.com</UserName>
                </request>
            </GetUserDetails>
        </soap12:Body>
    </soap12:Envelope>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| UserDetails | Complex | The list of users |

### UserDetails Attributes

| Name | Type | Description |
| --- | --- | --- |
| AccountAlias | String | Short code for a particular account. |
| UserName | String | User name, which is typically the email address. |
| EmailAddress | String | Email address for the user. |
| FirstName | String | First name of the user. |
| LastName | String | Last name of the user. |
| AlternateEmailAddress | String | Additional email address for the user. |
| Title | String | Job title of the user. |
| OfficeNumber | String | Office phone number of the user. |
| MobileNumber | String | Mobile phone number of the user. |
| AllowSMS | Boolean | Flag indicating whether this user can receive SMS messages. |
| FaxNumber | String | Fax number for the user. |
| SAMLUserName | String | Name used for single-sign-on process. |
| TimeZoneID | String | Time zone that the user resides in. |
| Roles | Integer[] | List of values indicating the roles assigned to this user.<br/>2 = Server Administrator<br/>3 = Billing Manager<br/>8 = DNS Manager<br/>9 = Account Administrator<br/>10 = Account Viewer<br/>12 = Network Manager<br/>13 = Security Manager<br/>14 = Server Operator |

### Examples

#### JSON

    {
      "UserDetails": {
        "AccountAlias":"1000",
        "UserName":"user1@company.com",
        "EmailAddress":"user1@company.com",
        "FirstName":"Ellie",
        "LastName":"User",
        "AlternateEmailAddress":"",
        "Title":"",
        "OfficeNumber":"",
        "MobileNumber":"",
        "AllowSMS":false,
        "FaxNumber":"",
        "SAMLUserName":null,
        "TimeZoneID":"Pacific Standard Time",
        "Roles":[8]
      },
      "Success":true,
      "Message":"User successfully located.",
      "StatusCode":0
    }

#### XML (REST)

    <UserDetailsResponse Success="true" Message="User successfully located." StatusCode="0">
        <UserDetails AccountAlias="1000"
          UserName="user1@company.com"
          EmailAddress="user1@company.com"
          FirstName="Ellie"
          LastName="User"
          AlternateEmailAddress=""
          Title=""
          OfficeNumber=""
          MobileNumber=""
          AllowSMS="false"
          FaxNumber=""
          TimeZoneID="Pacific Standard Time">
            <Roles>
                <int>8</int>
            </Roles>
        </UserDetails>
    </UserDetailsResponse>

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema">
        <soap:Body>
            <GetUserDetailsResponse xmlns="http://www.tier3.com/">
                <GetUserDetailsResult Success="true" Message="User successfully located." StatusCode="0">
                    <UserDetails AccountAlias="1000"
                      UserName="user1@company.com"
                      EmailAddress="user1@company.com"
                      FirstName="Ellie"
                      LastName="User"
                      AlternateEmailAddress=""
                      Title=""
                      OfficeNumber=""
                      MobileNumber=""
                      AllowSMS="false"
                      FaxNumber=""
                      TimeZoneID="Pacific Standard Time">
                        <Roles>
                            <int>8</int>
                        </Roles>
                    </UserDetails>
                </GetUserDetailsResult>
            </GetUserDetailsResponse>
        </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 5 | Resource Not Found.  Provided account alias does not exist. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1600 | Account Alias Required.  You must provide an account alias when calling this method. |
| 1700 | Email Address Required.  You must provide an email address when calling this method. |
| 1705 | User Not Found.  Provided user name does not exist. |
