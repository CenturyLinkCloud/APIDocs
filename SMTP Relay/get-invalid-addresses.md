{{{
  "title": "Get Invalid Addresses",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method will retrieve the list of invalid address responses that have been saved by the SMTP Relay system related to your domain.

## URL

    REST: https://api.ctl.io/REST/SMTPRelay/GetInvalidAddresses/<format> (format = XML | JSON)

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| DomainAlias | String | The domain to search for as the source of SMTP Relay errors. | Yes |
| StartDate | Date | This is the starting date to use for the query. This value is inclusive. | Yes |
| EndDate | Date | This is the ending date to use for the query. This value is inclusive. | Yes |

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

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| BadAddresses | List | The List of Bad Address entries containing the details of the rejected aliases. |
| Address | String | The destination email address which was rejected. |
| Reason | String | The reason reported for the rejection. |
| Server | String | The mail server which rejected the email. |
| LogDate | Datetime | The date and time the error was logged. |

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

| Status Code | Description |
| --- | --- |
| 0 | GetInvalidAddresses request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
