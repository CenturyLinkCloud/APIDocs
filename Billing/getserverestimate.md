{{{
  "title": "GetServerEstimate",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}


Gets the estimated monthly cost for a given server. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Billing/GetServerEstimate/&lt;format&gt; (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Billing.asmx?op=GetServerEstimate

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
      <td>Short code for a particular account. If not provided, then the API user's account is used.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>ServerName</td>
      <td>String</td>
      <td>Name given to the server.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON (REST)</h4>
<pre>{ <br />    "AccountAlias": "1000",<br />    "ServerName":"SVR1"<br />}</pre>

<h4>XML (REST)</h4>
<pre>&lt;ServerEstimateRequest&gt;

  &lt;AccountAlias&gt;RSDA&lt;/AccountAlias&gt;

  &lt;ServerName&gt;SVR1&lt;/ServerName&gt;

&lt;/ServerEstimateRequest&gt;

  </pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

  xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

  xmlns:soap12="http://www.w3.org/2003/05/soap-envelope"&gt;

&lt;soap12:Body&gt;

  &lt;GetServerEstimate xmlns="http://www.tier3.com/"&gt;

      &lt;name&gt;SVR1&lt;/name&gt;

  &lt;/GetServerEstimate&gt;

&lt;/soap12:Body&gt;

&lt;/soap12:Envelope&gt;    

</pre> 

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
      <td>MonthlyEstimate</td>
      <td>Decimal</td>
      <td>Estimated cost of this server given current rate of usage.</td>
    </tr>
    <tr>
      <td>MonthToDate</td>
      <td>Decimal</td>
      <td>Charges incurred up to today.</td>
    </tr>
    <tr>
      <td>CurrentHour</td>
      <td>Decimal</td>
      <td>Charges for the current hour of usage.</td>
    </tr>
    <tr>
      <td>PreviousHour</td>
      <td>Decimal</td>
      <td>Charges for the previous hour of usage.</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON (REST)</h4>
<pre>{<br />     "MonthlyEstimate":0,<br />     "MonthToDate":0,<br />     "CurrentHour":0,<br />     "PreviousHour":0,<br />     "Success":true,<br />     "Message":"OK",<br />     "StatusCode":0<br />}</pre>

<h4>XML (REST)</h4>
<pre>&lt;BillingResponse Success="true" 

  Message="OK" 

  StatusCode="0" 

  MonthlyEstimate="0" 

  MonthToDate="0" 

  CurrentHour="0" 

  PreviousHour="0" /&gt;

</pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" 

  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

  xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

  &lt;soap:Body&gt;

      &lt;GetServerEstimateResponse xmlns="http://www.tier3.com/"&gt;

          &lt;GetServerEstimateResult Success="true" 

              Message="OK" 

              StatusCode="0" 

              MonthlyEstimate="0" 

              MonthToDate="0" 

              CurrentHour="0" 

              PreviousHour="0" /&gt;

      &lt;/GetServerEstimateResponse&gt;

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
      <td>5</td>
      <td>Resource Does Not Exist. &nbsp;You must provide a valid server identifier when calling this method.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>541</td>
      <td>Hardware Group Not Found. &nbsp;You must provide a valid hardware group ID when calling this method.</td>
    </tr>
    <tr>
      <td>1800</td>
      <td>Account Not Found. &nbsp;You must provide a valid account alias when calling this method.</td>
    </tr>
  </tbody>
</table>
