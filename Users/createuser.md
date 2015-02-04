{{{
  "title": "CreateUser",
  "date": "11-12-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Create a new user within a given account. Calls to this operation must include an authorization cookie acquired from the <a href="/api-docs#authentication-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/User/CreateUser/<format>
    SOAP: https://api.tier3.com/SOAP/User.asmx?op=CreateUser

## Request

### Attributes

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Req.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>UserName</td>
      <td>String</td>
      <td>Unique username for the new user. Can be an email address or any other string value.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short code for a particular account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>EmailAddress</td>
      <td>String</td>
      <td>Email address of the new user.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>FirstName</td>
      <td>String</td>
      <td>First name of the new user.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Last Name</td>
      <td>String</td>
      <td>Last name of the new user.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>AlternateEmailAddress</td>
      <td>String</td>
      <td>Additional email address for the user.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Title</td>
      <td>String</td>
      <td>Job title of the user.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>OfficeNumber</td>
      <td>String</td>
      <td>Office phone number of the user.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>MobileNumber</td>
      <td>String</td>
      <td>Mobile phone number of the user.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>AllowSMSAlerts</td>
      <td>Boolean</td>
      <td>Flag determining whether this user can receive SMS messages.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>FaxNumber</td>
      <td>String</td>
      <td>Fax number of the user.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>SAMLUserName</td>
      <td>String</td>
      <td>String holding the value used during single-sign-on processes.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Roles</td>
      <td>Integer[]</td>
      <td>List of values indicating the roles assigned to this user.
        <br />
        <p>2 = Server Administrator
          <br />3 = Billing Manager
          <br />8 = DNS Manager
          <br />9 = Account Administrator
          <br />10 = Account Viewer
          <br />12 = Network Manager
          <br />13 = Security Manager
          <br />14 = Server Operator</p>
      </td>
      <td>No</td>
    </tr>
    <tr>
      <td>TimeZoneID</td>
      <td>String</td>
      <td>Time zone of the user. Timezone must be one of the values in <a href="#tz">the table below</a>, otherwise the value is set to the account"s Timezone.</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    { 

        "UserName":"user3",

        "AccountAlias":"1000", 

        "EmailAddress":"user3@company.com", 

        "FirstName":"Watson", 

        "LastName":"User", 

        "AlternateEmailAddress":null, 

        "Title":null, 

         "OfficeNumber":null, 

        "MobileNumber":null,

          "AllowSMSAlerts":false, 

        "FaxNumber":null, 

        "SAMLUserName":null, 

        "Roles":[2,8], 

        "TimeZoneID":null 

    }

#### XML (REST)

    <CreateUserRequest> 

        <UserName>user3</UserName> 

        <AccountAlias>1000</AccountAlias> 

        <EmailAddress>user3@company.com</EmailAddress> 

        <FirstName>Watson</FirstName> 

        <LastName>User</LastName> 

        <AlternateEmailAddress></AlternateEmailAddress> 

        <Title></Title> 

        <OfficeNumber></OfficeNumber> 

        <MobileNumber></MobileNumber> 

        <AllowSMSAlerts>false</AllowSMSAlerts>

        <FaxNumber></FaxNumber> 

        <SAMLUserName></SAMLUserName> 

        <Roles><int>8</int></Roles> 

        <TimeZoneID></TimeZoneID> 

    </CreateUserRequest>

#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

        xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

        xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">

      <soap12:Body>

        <CreateUser xmlns="http://www.tier3.com/">

          <request>

            <UserName>user3</UserName> 

            <AccountAlias>1000</AccountAlias> 

            <EmailAddress>user3@company.com</EmailAddress> 

            <FirstName>Watson</FirstName> 

            <LastName>User</LastName> 

            <AlternateEmailAddress></AlternateEmailAddress> 

            <Title></Title> 

            <OfficeNumber></OfficeNumber> 

            <MobileNumber></MobileNumber> 

            <AllowSMSAlerts>false</AllowSMSAlerts>

            <FaxNumber></FaxNumber> 

            <SAMLUserName></SAMLUserName> 

            <Roles><int>8</int></Roles> 

            <TimeZoneID></TimeZoneID> 

          </request>

        </CreateUser>

      </soap12:Body>

    </soap12:Envelope>  

## Response

### Attributes

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Success</td>
      <td>Boolean</td>
      <td>True if the request was successful, otherwise False.</td>
    </tr>
    <tr>
      <td>Message</td>
      <td>String</td>
      <td>A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result.</td>
    </tr>
    <tr>
      <td>StatusCode</td>
      <td>Int</td>
      <td>This value will help to identify any errors which were encountered while processing the request. The value of "0" indicates success, all non-zero StatusCodes indicate an error state.</td>
    </tr>
    <tr>
      <td>UserDetails</td>
      <td>Complex</td>
      <td>The details of the newly created user.</td>
    </tr>
  </tbody>
</table>

### UserDetails Attributes

<table>
  <thead>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short code for a particular account.</td>
    </tr>
    <tr>
      <td>UserName</td>
      <td>String</td>
      <td>User name, which is typically the email address.</td>
    </tr>
    <tr>
      <td>EmailAddress</td>
      <td>String</td>
      <td>Email address for the user.</td>
    </tr>
    <tr>
      <td>FirstName</td>
      <td>String</td>
      <td>First name of the user.</td>
    </tr>
    <tr>
      <td>LastName</td>
      <td>String</td>
      <td>Last name of the user.</td>
    </tr>
    <tr>
      <td>AlternateEmailAddress</td>
      <td>String</td>
      <td>Additional email address for the user.</td>
    </tr>
    <tr>
      <td>Title</td>
      <td>String</td>
      <td>Job title of the user.</td>
    </tr>
    <tr>
      <td>OfficeNumber</td>
      <td>String</td>
      <td>Office phone number of the user.</td>
    </tr>
    <tr>
      <td>MobileNumber</td>
      <td>String</td>
      <td>Mobile phone number of the user.</td>
    </tr>
    <tr>
      <td>AllowSMS</td>
      <td>Boolean</td>
      <td>Flag indicating whether this user can receive SMS messages.</td>
    </tr>
    <tr>
      <td>FaxNumber</td>
      <td>String</td>
      <td>Fax number for the user.</td>
    </tr>
    <tr>
      <td>SAMLUserName</td>
      <td>String</td>
      <td>Name used for single-sign-on process.</td>
    </tr>
    <tr>
      <td>TimeZoneID</td>
      <td>String</td>
      <td>Time zone that the user resides in.</td>
    </tr>
    <tr>
      <td>Roles</td>
      <td>Integer[]</td>
      <td>List of values indicating the roles assigned to this user.
        <br />
        <p>2 = Server Admin
          <br />8 = Domain Admin
          <br />9 = Account Admin</p>
      </td>
    </tr>
  </tbody>
</table>

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

            "Title":null,

            "OfficeNumber":null,

            "MobileNumber":null,

            "AllowSMS":false,

            "FaxNumber":null,

            "SAMLUserName":null,

            "TimeZoneID":"Pacific Standard Time",

            "Roles":[2,8]

         },

        "Success":true,

        "Message":"User successfully created.",

        "StatusCode":0

    }


#### XML (REST)

    <UserDetailsResponse Success="true" Message="User successfully created." StatusCode="0">

        <UserDetails AccountAlias="1000" 

            UserName="user3@company.com" 

            EmailAddress="user3@company.com" 

            FirstName="Watson" 

            LastName="Demo" 

            AlternateEmailAddress="" 

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

            <CreateUserResponse xmlns="http://www.tier3.com/">

                <CreateUserResult Success="true" Message="User successfully created." StatusCode="0">

                    <UserDetails AccountAlias="1000" 

                        UserName="user3@company.com" 

                        EmailAddress="user3@company.com" 

                        FirstName="Watson" 

                        LastName="Demo" 

                        AlternateEmailAddress="" 

                        OfficeNumber="" 

                        MobileNumber="" 

                        AllowSMS="false"

                        FaxNumber="" 

                        TimeZoneID="Pacific Standard Time">

                        <Roles><int>8</int></Roles>

                    </UserDetails>

                </CreateUserResult>

            </CreateUserResponse>

        </soap:Body>

    </soap:Envelope>

### Status Codes

<table>
  <thead>
    <tr>
      <th>Status Code</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;Provided account alias does not exist.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1600</td>
      <td>Account Alias Required. &nbsp;You must provide an account alias when calling this method.</td>
    </tr>
    <tr>
      <td>1700</td>
      <td>Email Address Required. &nbsp;You must provide an email address when calling this method.</td>
    </tr>
    <tr>
      <td>1701</td>
      <td>User Already Exists. &nbsp;You must provide a unique user name when calling this method.</td>
    </tr>
    <tr>
      <td>1702</td>
      <td>First Name Required. &nbsp;You must provide user"s first name when calling this method.</td>
    </tr>
    <tr>
      <td>1703</td>
      <td>Last Name Required. &nbsp;You must provide a user"s last name when calling this method.</td>
    </tr>
    <tr>
      <td>1706</td>
      <td>Invalid User Roles. &nbsp;You must provide a valid user role (2, 8, and 9) when calling this method.</td>
    </tr>
    <tr>
      <td>1707</td>
      <td>Invalid Email Address. &nbsp;You must provide a valid email address.</td>
    </tr>
  </tbody>
</table>
<p>
  <a name="tz"></a>
</p>

### Valid Timezone Entries

<table>
  <thead>
    <tr>
      <th>Timezone Value</th>
    </tr>
  </thead>
  <tbody>
    
    <tr>
      <td>Dateline Standard Time
        <br /> UTC-11
        <br /> Hawaiian Standard Time
        <br /> Alaskan Standard Time
        <br /> Pacific Standard Time (Mexico)
        <br /> Pacific Standard Time
        <br /> US Mountain Standard Time
        <br /> Mountain Standard Time (Mexico)
        <br /> Mountain Standard Time
        <br /> Central America Standard Time
        <br /> Central Standard Time
        <br /> Central Standard Time(Mexico)
        <br /> Canada Central Standard Time
        <br /> SA Pacific Standard Time
        <br /> Eastern Standard Time
        <br /> US Eastern Standard Time
        <br /> Venezuela Standard Time
        <br /> Paraguay Standard Time
        <br /> Atlantic Standard Time
        <br /> Central Brazilian Standard Time
        <br /> SA Western Standard Time
        <br /> Pacific SA Standard Time
        <br /> Newfoundland Standard Time
        <br /> E. South America Standard Time
        <br /> Argentina Standard Time
        <br /> SA Eastern Standard Time
        <br /> Greenland Standard Time
        <br /> Montevideo Standard Time
        <br /> Bahia Standard Time
        <br /> UTC-02
        <br /> Mid-Atlantic Standard Time
        <br /> Azores Standard Time
        <br /> Cape Verde Standard Time
        <br /> Morocco Standard Time
        <br /> UTC
        <br /> GMT Standard Time
        <br /> Greenwich Standard Time
        <br /> W. Europe Standard Time
        <br /> Central Europe Standard Time
        <br /> Romance Standard Time
        <br /> Central European Standard Time
        <br /> W. Central Africa Standard Time
        <br /> Namibia Standard Time
        <br /> Jordan Standard Time
        <br /> GTB Standard Time
        <br /> Middle East Standard Time
        <br /> Egypt Standard Time
        <br /> Syria Standard Time
        <br /> South Africa Standard Time
        <br /> FLE Standard Time
        <br /> Turkey Standard Time
        <br /> Israel Standard Time
        <br /> E. Europe Standard Time
        <br /> Arabic Standard Time
        <br /> Kaliningrad Standard Time
        <br /> Arab Standard Time
        <br /> E. Africa Standard Time
        <br /> Iran Standard Time
        <br /> Arabian Standard Time
        <br /> Azerbaijan Standard Time
        <br /> Russian Standard Time
        <br /> Mauritius Standard Time
        <br /> Georgian Standard Time
        <br /> Caucasus Standard Time
        <br /> Afghanistan Standard Time
        <br /> Pakistan Standard Time
        <br /> West Asia Standard Time
        <br /> India Standard Time
        <br /> Sri Lanka Standard Time
        <br /> Nepal Standard Time
        <br /> Central Asia Standard Time
        <br /> Bangladesh Standard Time
        <br /> Ekaterinburg Standard Time
        <br /> Myanmar Standard Time
        <br /> SE Asia Standard Time
        <br /> N. Central Asia Standard Time
        <br /> China Standard Time
        <br /> North Asia Standard Time
        <br /> Singapore Standard Time
        <br /> W. Australia Standard Time
        <br /> Taipei Standard Time
        <br /> Ulaanbaatar Standard Time
        <br /> North Asia East Standard Time
        <br /> Tokyo Standard Time
        <br /> Korea Standard Time
        <br /> Cen. Australia Standard Time
        <br /> AUS Central Standard Time
        <br /> E. Australia Standard Time
        <br /> AUS Eastern Standard Time
        <br /> West Pacific Standard Time
        <br /> Tasmania Standard Time
        <br /> Yakutsk Standard Time
        <br /> Central Pacific Standard Time
        <br /> Vladivostok Standard Time
        <br /> New Zealand Standard Time
        <br /> UTC+12
        <br /> Fiji Standard Time
        <br /> Magadan Standard Time
        <br /> Kamchatka Standard Time
        <br /> Tonga Standard Time
        <br /> Samoa Standard Time</td>
    </tr>
  </tbody>
</table>