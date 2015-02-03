{{{
  "title": "Get Invalid Addresses",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}

GetInvalidAddresses
<p>This method will retrieve the list of invalid address responses that have been saved by the SMTP Relay system related to your domain.
  <br />
  <br /><strong>URL:</strong>
</p>
<pre>https://api.tier3.com/REST/SMTPRelay/GetInvalidAddresses/&lt;format&gt;</pre>
<p>
  <br />
  <br /><strong>GetInvalidAddresses Request Attributes:</strong>
</p>
<table>
  <tbody>
    <tr>
      <td><strong>Attribute Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Required</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
    <tr>
      <td>DomainAlias</td>
      <td>String</td>
      <td>Yes</td>
      <td>The domain to search for as the source of SMTP Relay errors.</td>
    </tr>
    <tr>
      <td>StartDate</td>
      <td>Date</td>
      <td>Yes</td>
      <td>This is the starting date to use for the query. This value is inclusive.</td>
    </tr>
    <tr>
      <td>EndDate</td>
      <td>Date</td>
      <td>Yes</td>
      <td>This is the ending date to use for the query. This value is inclusive.</td>
    </tr>
  </tbody>
</table>
<p>
  <br /><strong>Example Messages:</strong>&nbsp;<strong>XML:</strong>
</p>
<pre>&lt;InvalidAddressRequest&gt;

  &lt;DomainAlias&gt;mydomain&lt;/DomainAlias&gt;

  &lt;StartDate&gt;2010-09-01&lt;/StartDate&gt;

  &lt;EndDate&gt;2010-09-02&lt;/EndDate&gt;

&lt;/InvalidAddressRequest&gt;

</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

  "DomainAlias":"mydomain",

  "StartDate":"\/Date(1261014726677)\/",

  "EndDate":"\/Date(1261045879270)\/"

}</pre>
<p>
  <br />
  <br /><strong>Response Attributes:</strong>
</p>
<table>
  <tbody>
    <tr>
      <td><strong>Attribute Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
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
      <td>BadAddresses</td>
      <td>List</td>
      <td>The List of Bad Address entries containing the details of the rejected aliases.</td>
    </tr>
    <tr>
      <td>Address</td>
      <td>String ||The destination email address which was rejected.</td>
    </tr>
    <tr>
      <td>Reason</td>
      <td>String</td>
      <td>The reason reported for the rejection.</td>
    </tr>
    <tr>
      <td>Server</td>
      <td>String</td>
      <td>The mail server which rejected the email.</td>
    </tr>
    <tr>
      <td>LogDate</td>
      <td>Datetime</td>
      <td>The date and time the error was logged.</td>
    </tr>
  </tbody>
</table>
<p>
  <br /><strong>Example Responses:</strong>&nbsp;<strong>XML:</strong>
</p>
<pre>&lt;InvalidAddressResponse Success="true" Message="GetInvalidAddresses completed successfully" StatusCode="0"&gt;  

  &lt;BadAddresses&gt;    

    &lt;BadAddress&gt;      

      &lt;Address&gt;user@xyz.net&lt;/Address&gt;      

      &lt;Reason&gt;mydomain.com sender, but not from mydomain.com-approved relay.&lt;/Reason&gt;      

      &lt;Server&gt;mail2.xyz.net&lt;/Server&gt;      

      &lt;LogDate&gt;2010-09-01T19:52:06.677&lt;/LogDate&gt;    

    &lt;/BadAddress&gt;    

    &lt;BadAddress&gt;      

      &lt;Address&gt;user@mail.com&lt;/Address&gt;      

      &lt;Reason&gt;00.000.000.000 is not allowed to send mail for service@mydomain.com' : Reason: mechanism&lt;/Reason&gt;

      &lt;Server&gt;mx.mail.com&lt;/Server&gt;      

      &lt;LogDate&gt;2010-09-02T04:31:19.27&lt;/LogDate&gt;    

    &lt;/BadAddress&gt;

  &lt;/BadAddresses&gt;

&lt;/InvalidAddressResponse&gt;

</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

  "BadAddresses":

  [

    {

      "Address":" user@xyz.net ",

      "Reason":"mydomain.com sender, but not from mydomain.com-approved relay.",

      "Server":"mail2.xyz.net",

      "LogDate":"\/Date(1261014726677)\/"

    },

    {

      "Address":"user@mail.com",

      "Reason":"00.000.000.000 is not allowed to send mail for \u0027service@mydomain.com\u0027 : Reason: mechanism",

      "Server":"mx.mail.com",

      "LogDate":"\/Date(1261045879270)\/"

    }

  ],

  "Success":true,

  "Message":"GetInvalidAddresses completed successfully",

  "StatusCode":0 

}</pre>
<p>
  <br />
  <br /><strong>Valid Status Codes returned by the GetInvalidAddresses Method:</strong>
</p>
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
      <td>GetInvalidAddresses request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>