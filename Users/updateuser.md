{{{
  "title": "UpdateUser",
  "date": "11-12-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Update a specific user within a given account. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/User/UpdateUser/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/User.asmx?op=UpdateUser

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| UserName | String | User name, which is typically the email address. | Yes |
| EmailAddress | String | Email address of the new user. | Yes |
| FirstName | String | First name of the new user. | Yes |
| Last Name | String | Last name of the new user. | Yes |
| AlternateEmailAddress | String | Additional email address for the user. | No |
| Title | String | Job title of the user. | No |
| OfficeNumber | String | Office phone number of the user. | No |
| MobileNumber | String | Mobile phone number of the user. | No |
| AllowSMSAlerts | Boolean | Flag determining whether this user can receive SMS messages. | No |
| FaxNumber | String | Fax number of the user. | No |
| SAMLUserName | String | String holding the value used during single-sign-on processes. | No |
| TimeZoneID | String | Time zone of the user. Timezone must be one of the values in the list below, otherwise the value is set to the account's Timezone. | No |
| Roles | Integer[] | List of values indicating the roles assigned to this user.<br/>2 = Server Administrator<br/>3 = Billing Manager<br/>8 = DNS Manager<br/>9 = Account Administrator<br/>10 = Account Viewer<br/>12 = Network Manager<br/>13 = Security Manager<br/>14 = Server Operator | No |

### Examples

#### JSON

    {
      "UserName":"user3@company.com",
      "EmailAddress":"user3@company.com",
      "FirstName":"Watson",
      "LastName":"User",
      "AlternateEmailAddress":null,
      "Title":"President",
      "OfficeNumber":null,
      "MobileNumber":null,
      "AllowSMSAlerts":false,
      "FaxNumber":null,
      "SAMLUserName":null,
      "Roles":[8],
      "TimeZoneID":null
    }

#### XML (REST)

    <UpdateUserRequest>
        <UserName>user3@company.com</UserName>
        <EmailAddress>user3@company.com</EmailAddress>
        <FirstName>Watson</FirstName>
        <LastName>User</LastName>
        <AlternateEmailAddress></AlternateEmailAddress>
        <Title>President</Title>
        <OfficeNumber></OfficeNumber>
        <MobileNumber></MobileNumber>
        <AllowSMSAlerts>false</AllowSMSAlerts>
        <FaxNumber></FaxNumber>
        <SAMLUserName></SAMLUserName>
        <Roles><int>8</int></Roles>
        <TimeZoneID></TimeZoneID>
    </UpdateUserRequest>

#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema"
      xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
        <soap12:Body>
            <UpdateUser xmlns="http://www.tier3.com/">
                <request>
                    <UserName>user3@company.com</UserName>
                    <EmailAddress>user3@company.com</EmailAddress>
                    <FirstName>Watson</FirstName>
                    <LastName>User</LastName>
                    <AlternateEmailAddress></AlternateEmailAddress>
                    <Title>President</Title>
                    <OfficeNumber></OfficeNumber>
                    <MobileNumber></MobileNumber>
                    <AllowSMSAlerts>false</AllowSMSAlerts>
                    <FaxNumber></FaxNumber>
                    <SAMLUserName></SAMLUserName>
                    <Roles><int>8</int></Roles>
                    <TimeZoneID></TimeZoneID>
                </request>
            </UpdateUser>
        </soap12:Body>
    </soap12:Envelope>  


## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| UserDetails | Complex | The details of the updated user. |

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
| Roles | Integer[] | List of values indicating the roles assigned to this user.<br/>2 = Server Admin<br/>8 = Domain Admin<br/>9 = Account Admin |

### Examples

#### JSON

    {
      "UserDetails":
        {
          "AccountAlias":"1000",
          "UserName":"user3@company.com",
          "EmailAddress":"user3@company.com",
          "FirstName":"Watson",
          "LastName":"Demo",
          "AlternateEmailAddress":null,
          "Title":'President',
          "OfficeNumber":null,
          "MobileNumber":null,
          "AllowSMS":false,
          "FaxNumber":null,
          "SAMLUserName":null,
          "TimeZoneID":"Pacific Standard Time",
          "Roles":[8]
         },
      "Success":true,
      "Message":"User successfully updated.",
      "StatusCode":0
    }

#### XML (REST)

    <UserDetailsResponse Success="true" Message="User successfully updated." StatusCode="0">
        <UserDetails AccountAlias="1000"
          UserName="user3@company.com"
          EmailAddress="user3@company.com"
          FirstName="Watson"
          LastName="Demo"
          AlternateEmailAddress=""
          Title="President"
          OfficeNumber=""
          MobileNumber=""
          AllowSMS="false"
          FaxNumber=""
          TimeZoneID="Pacific Standard Time">
            <Roles><int>8</int></Roles>
        </UserDetails>
    </UserDetailsResponse>


#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema">
        <soap:Body>
            <UpdateUserResponse xmlns="http://www.tier3.com/">
                <UpdateUserResult Success="true" Message="User successfully updated." StatusCode="0">
                    <UserDetails AccountAlias="1000"
                      UserName="user3@company.com"
                      EmailAddress="user3@company.com"
                      FirstName="Watson"
                      LastName="Demo"
                      AlternateEmailAddress=""
                      Title="President"
                      OfficeNumber=""
                      MobileNumber=""
                      AllowSMS="false"
                      FaxNumber=""
                      TimeZoneID="Pacific Standard Time">
                        <Roles><int>8</int></Roles>
                    </UserDetails>
                </UpdateUserResult>
            </UpdateUserResponse>
        </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1700 | Email Address Required.  You must provide an email address when calling this method. |
| 1702 | First Name Required.  You must provide user's first name when calling this method. |
| 1703 | Last Name Required.  You must provide a user's last name when calling this method. |
| 1704 | Username Required.  You must provide a valid username when calling this method. |
| 1705 | User Not Found.  This user was not found in the system. |
| 1706 | Invalid User Roles.  You must provide a valid user role (2, 8, and 9) when calling this method. |

### Valid Timezone Entries

- Dateline Standard Time
- UTC-11
- Hawaiian Standard Time
- Alaskan Standard Time
- Pacific Standard Time (Mexico)
- Pacific Standard Time
- US Mountain Standard Time
- Mountain Standard Time (Mexico)
- Mountain Standard Time
- Central America Standard Time
- Central Standard Time
- Central Standard Time(Mexico)
- Canada Central Standard Time
- SA Pacific Standard Time
- Eastern Standard Time
- US Eastern Standard Time
- Venezuela Standard Time
- Paraguay Standard Time
- Atlantic Standard Time
- Central Brazilian Standard Time
- SA Western Standard Time
- Pacific SA Standard Time
- Newfoundland Standard Time
- E. South America Standard Time
- Argentina Standard Time
- SA Eastern Standard Time
- Greenland Standard Time
- Montevideo Standard Time
- Bahia Standard Time
- UTC-02
- Mid-Atlantic Standard Time
- Azores Standard Time
- Cape Verde Standard Time
- Morocco Standard Time
- UTC
- GMT Standard Time
- Greenwich Standard Time
- W. Europe Standard Time
- Central Europe Standard Time
- Romance Standard Time
- Central European Standard Time
- W. Central Africa Standard Time
- Namibia Standard Time
- Jordan Standard Time
- GTB Standard Time
- Middle East Standard Time
- Egypt Standard Time
- Syria Standard Time
- South Africa Standard Time
- FLE Standard Time
- Turkey Standard Time
- Israel Standard Time
- E. Europe Standard Time
- Arabic Standard Time
- Kaliningrad Standard Time
- Arab Standard Time
- E. Africa Standard Time
- Iran Standard Time
- Arabian Standard Time
- Azerbaijan Standard Time
- Russian Standard Time
- Mauritius Standard Time
- Georgian Standard Time
- Caucasus Standard Time
- Afghanistan Standard Time
- Pakistan Standard Time
- West Asia Standard Time
- India Standard Time
- Sri Lanka Standard Time
- Nepal Standard Time
- Central Asia Standard Time
- Bangladesh Standard Time
- Ekaterinburg Standard Time
- Myanmar Standard Time
- SE Asia Standard Time
- N. Central Asia Standard Time
- China Standard Time
- North Asia Standard Time
- Singapore Standard Time
- W. Australia Standard Time
- Taipei Standard Time
- Ulaanbaatar Standard Time
- North Asia East Standard Time
- Tokyo Standard Time
- Korea Standard Time
- Cen. Australia Standard Time
- AUS Central Standard Time
- E. Australia Standard Time
- AUS Eastern Standard Time
- West Pacific Standard Time
- Tasmania Standard Time
- Yakutsk Standard Time
- Central Pacific Standard Time
- Vladivostok Standard Time
- New Zealand Standard Time
- UTC+12
- Fiji Standard Time
- Magadan Standard Time
- Kamchatka Standard Time
- Tonga Standard Time
- Samoa Standard Time
