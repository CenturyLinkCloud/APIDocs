{{{
  "title": "GetAccountSummary",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets monthly and hourly charges and estimates for a given account or collection of accounts. Calls to this operation must include an authorization cookie acquired from the <a href="/api-docs#authentication-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Billing/GetAccountSummary/<format> (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Billing.asmx?op=GetAccountSummary

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
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short code for a particular account.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

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
      <td>MonthlyEstimates</td>
      <td>Decimal</td>
      <td>The current estimate of total hourly charges, assuming the current hourly run rate.</td>
    </tr>
    <tr>
      <td>MonthToDate</td>
      <td>Decimal</td>
      <td>The total of actual hourly charges incurred thus far.</td>
    </tr>
    <tr>
      <td>CurrentHour</td>
      <td>Decimal</td>
      <td>The total charges incurred during the current hour.</td>
    </tr>
    <tr>
      <td>PreviousHour</td>
      <td>Decimal</td>
      <td>The total charges incurred during the previous hour.</td>
    </tr>
    <tr>
      <td>OneTimeCharges</td>
      <td>Decimal</td>
      <td>The total one time charges incurred this month (this would be for non-recurring charges such as domain name registration, SSL Certificates, etc.).</td>
    </tr>
    <tr>
      <td>MonthToDateTotal</td>
      <td>Decimal</td>
      <td>The total charges incurred this month to date, including One Time Charges.</td>
    </tr>
  </tbody>
</table>

### Examples

####JSON (REST)

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
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1800</td>
      <td>Account Not Found. &nbsp;You must provide a valid account alias when calling this method.</td>
    </tr>
  </tbody>
</table>
