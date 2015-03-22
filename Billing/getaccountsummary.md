{{{
  "title": "GetAccountSummary",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets monthly and hourly charges and estimates for a given account or collection of accounts. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/Billing/GetAccountSummary/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Billing.asmx?op=GetAccountSummary

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | Short code for a particular account. | Yes |

### Examples

#### JSON (REST)

    {
      "AccountAlias": "1000"
    }

#### XML (REST)

    <BillingRequest>
        <AccountAlias>1000</AccountAlias>
    </BillingRequest>

#### XML (SOAP)

    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:xsd="http://www.w3.org/2001/XMLSchema"
          xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
      <GetAccountSummary xmlns="http://www.tier3.com/">
        <request>
           <accountAlias>1000</accountAlias>
        </request>
      </GetAccountSummary>
    </soap:Body>
    </soap:Envelope>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| MonthlyEstimates | Decimal | The current estimate of total hourly charges, assuming the current hourly run rate. |
| MonthToDate | Decimal | The total of actual hourly charges incurred thus far. |
| CurrentHour | Decimal | The total charges incurred during the current hour. |
| PreviousHour | Decimal | The total charges incurred during the previous hour. |
| OneTimeCharges | Decimal | The total one time charges incurred this month (this would be for non-recurring charges such as domain name registration, SSL Certificates, etc.). |
| MonthToDateTotal | Decimal | The total charges incurred this month to date, including One Time Charges. |

### Examples

#### JSON (REST)

    {
      "OneTimeCharges":0,
      "MonthToDateTotal":2.000000,
      "MonthlyEstimate":2.000000,
      "MonthToDate":2.000000,
      "CurrentHour":0.0,
      "PreviousHour":0.0,
      "Success":true,
      "Message":"OK",
      "StatusCode":0
    }

#### XML (REST)

    <BillingSummmaryResponse
      Success="true"
      Message="OK"
      StatusCode="0"
      MonthlyEstimate="161.870000"
      MonthToDate="82.050000"
      CurrentHour="0.223600"
      PreviousHour="0.223600"
      OneTimeCharges="0"
      MonthToDateTotal="82.050000" />

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema">
        <soap:Body>
            <GetAccountSummaryResponse xmlns="http://www.tier3.com/">
                <GetAccountSummaryResult
                    Success="true"
                    Message="OK"
                    StatusCode="0"
                    MonthlyEstimate="2.000000"
                    MonthToDate="2.000000"
                    CurrentHour="0.0" 
                    PreviousHour="0.0"
                    OneTimeCharges="0"
                    MonthToDateTotal="2.000000" />
            </GetAccountSummaryResponse>
        </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1800 | Account Not Found.  You must provide a valid account alias when calling this method. |
