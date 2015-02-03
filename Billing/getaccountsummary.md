{{{
  "title": "GetAccountSummary",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets monthly and hourly charges and estimates for a given account or collection of accounts. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Billing/GetAccountSummary/&lt;format&gt; (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Billing.asmx?op=GetAccountSummary

## Request
### Attributes
<table>
    <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Required</th>
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
<h4>JSON (REST)</h4>
<pre>{ <br />    "AccountAlias": "1000"<br />}</pre>

<h4>XML (REST)</h4>
<pre>&lt;BillingRequest&gt;<br />     &lt;AccountAlias&gt;1000&lt;/AccountAlias&gt;<br />&lt;/BillingRequest&gt;</pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

      xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

      xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"&gt;

&lt;soap:Body&gt;

  &lt;GetAccountSummary xmlns="http://www.tier3.com/"&gt;

    &lt;request&gt;

       &lt;accountAlias&gt;1000&lt;/accountAlias&gt;

    &lt;/request&gt;

  &lt;/GetAccountSummary&gt;

&lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;    

</pre> 

## Response
### Attributes
<table>
  <tbody>
    <tr>
      <td><strong>Name</strong>
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
<h4>JSON (REST)</h4>
<pre>{<br />     "OneTimeCharges":0,<br />     "MonthToDateTotal":2.000000,<br />     "MonthlyEstimate":2.000000,<br />     "MonthToDate":2.000000,<br />     "CurrentHour":0.0,<br />     "PreviousHour":0.0,<br />     "Success":true,<br />     "Message":"OK",<br />     "StatusCode":0<br />}</pre>

<h4>XML (REST)</h4>
<pre>&lt;BillingSummmaryResponse 

  Success="true" 

  Message="OK" 

  StatusCode="0" 

  MonthlyEstimate="161.870000" 

  MonthToDate="82.050000" 

  CurrentHour="0.223600" 

  PreviousHour="0.223600" 

  OneTimeCharges="0" 

  MonthToDateTotal="82.050000" /&gt;

  </pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" 

  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

  xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

  &lt;soap:Body&gt;

      &lt;GetAccountSummaryResponse xmlns="http://www.tier3.com/"&gt;

          &lt;GetAccountSummaryResult 

              Success="true" 

              Message="OK" 

              StatusCode="0" 

              MonthlyEstimate="2.000000" 

              MonthToDate="2.000000" 

              CurrentHour="0.0" 

              PreviousHour="0.0" 

              OneTimeCharges="0" 

              MonthToDateTotal="2.000000" /&gt;

      &lt;/GetAccountSummaryResponse&gt;

  &lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;

</pre>

### Status Codes
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
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1800</td>
      <td>Account Not Found. &nbsp;You must provide a valid account alias when calling this method.</td>
    </tr>
  </tbody>
</table>
