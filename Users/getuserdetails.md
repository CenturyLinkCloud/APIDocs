{{{
  "title": "GetUserDetails",
  "date": "11-12-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

GetUserDetails
<p>Gets the details of a specific user associated with a given account. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>
</p>
URL
<pre>REST: https://api.tier3.com/REST/User/GetUserDetails/&lt;format&gt; (format = XML | JSON) <br />SOAP: https://api.tier3.com/SOAP/User.asmx?op=GetUserDetails </pre> Request
<h3>Attributes</h3>
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
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short code for a particular account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>UserName</td>
      <td>String</td>
      <td>User name, which is typically the email address.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON (REST)</h4>
<pre>{ <br />    "AccountAlias": "1000", "UserName": "user1@company.com"<br />}</pre>
<h4>XML (REST)</h4>
<pre>&lt;GetUserRequest&gt;&lt;AccountAlias&gt;RSDA&lt;/AccountAlias&gt;&lt;UserName&gt;user1@company.com&lt;/UserName&gt;&lt;/GetUserRequest&gt;</pre>
<h4>XML (SOAP)</h4>
<pre>&lt;soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

        xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

        xmlns:soap12="http://www.w3.org/2003/05/soap-envelope"&gt;

  &lt;soap12:Body&gt;

    &lt;GetUserDetails xmlns="http://www.tier3.com/"&gt;

      &lt;request&gt;

        &lt;AccountAlias&gt;1000&lt;/AccountAlias&gt;

        &lt;UserName&gt;user1@company.com&lt;/UserName&gt;

      &lt;/request&gt;

    &lt;/GetUserDetails&gt;

  &lt;/soap12:Body&gt;

&lt;/soap12:Envelope&gt;   

</pre> Response
<h3>Attributes</h3>
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
      <td>This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state.</td>
    </tr>
    <tr>
      <td>UserDetails</td>
      <td>Complex</td>
      <td>The list of users</td>
    </tr>
  </tbody>
</table>
<h3>UserDetails Attributes</h3>
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
        <p>2 = Server Administrator
          <br />3 = Billing Manager
          <br />8 = DNS Manager
          <br />9 = Account Administrator
          <br />10 = Account Viewer
          <br />12 = Network Manager
          <br />13 = Security Manager
          <br />14 = Server Operator</p>
      </td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON (REST)</h4>
<pre>{

        "UserDetails":

            {

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

    </pre>
<h4>XML (REST)</h4>
<pre>&lt;UserDetailsResponse Success="true" Message="User successfully located." StatusCode="0"&gt;

    &lt;UserDetails AccountAlias="1000" 

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

        TimeZoneID="Pacific Standard Time"&gt;

        &lt;Roles&gt;

            &lt;int&gt;8&lt;/int&gt;

        &lt;/Roles&gt;

    &lt;/UserDetails&gt;

&lt;/UserDetailsResponse&gt;

    </pre>
<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" 

    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

    xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

    &lt;soap:Body&gt;

        &lt;GetUserDetailsResponse xmlns="http://www.tier3.com/"&gt;

            &lt;GetUserDetailsResult Success="true" Message="User successfully located." StatusCode="0"&gt;

                &lt;UserDetails AccountAlias="1000" 

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

                    TimeZoneID="Pacific Standard Time"&gt;

                    &lt;Roles&gt;

                        &lt;int&gt;8&lt;/int&gt;

                    &lt;/Roles&gt;

                &lt;/UserDetails&gt;

            &lt;/GetUserDetailsResult&gt;

        &lt;/GetUserDetailsResponse&gt;

    &lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;

</pre>
<h3>Status Codes</h3>
<table>
  <tbody>
    <tr>
      <td><strong>Status Code</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
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
      <td>1705</td>
      <td>User Not Found. &nbsp;Provided user name does not exist.</td>
    </tr>
  </tbody>
</table>