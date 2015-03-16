{{{
  "title": "Get Invalid Addresses",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method will retrieve the list of invalid address responses that have been saved by the SMTP Relay system related to your domain.

## URL

    REST: https://api.ctl.io/REST/SMTPRelay/GetInvalidAddresses/<format>

## Request

### Attributes

<table>
  <tbody>
    <tr>
      <thead>
      <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
        <th>Req.</th>
      </tr>
    </thead>
    <tbody>
    </tr>
    <tr>
      <td>DomainAlias</td>
      <td>String</td>
      <td>The domain to search for as the source of SMTP Relay errors.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>StartDate</td>
      <td>Date</td>
      <td>This is the starting date to use for the query. This value is inclusive.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>EndDate</td>
      <td>Date</td>
      <td>This is the ending date to use for the query. This value is inclusive.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "DomainAlias":"mydomain",

      "StartDate":"\/Date(1261014726677)\/",

      "EndDate":"\/Date(1261045879270)\/"

    }

#### XML

    <InvalidAddressRequest>

      <DomainAlias>mydomain</DomainAlias>

      <StartDate>2010-09-01</StartDate>

      <EndDate>2010-09-02</EndDate>

    </InvalidAddressRequest>

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

### Examples

#### JSON

    {

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

    }

#### XML

    <InvalidAddressResponse Success="true" Message="GetInvalidAddresses completed successfully" StatusCode="0">  

      <BadAddresses>    

        <BadAddress>      

          <Address>user@xyz.net</Address>      

          <Reason>mydomain.com sender, but not from mydomain.com-approved relay.</Reason>      

          <Server>mail2.xyz.net</Server>      

          <LogDate>2010-09-01T19:52:06.677</LogDate>    

        </BadAddress>    

        <BadAddress>      

          <Address>user@mail.com</Address>      

          <Reason>00.000.000.000 is not allowed to send mail for service@mydomain.com' : Reason: mechanism</Reason>

          <Server>mx.mail.com</Server>      

          <LogDate>2010-09-02T04:31:19.27</LogDate>    

        </BadAddress>

      </BadAddresses>

    </InvalidAddressResponse>

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