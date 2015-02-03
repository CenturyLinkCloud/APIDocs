{{{
  "title": "GetBillingHistory",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}


Gets the entire billing history for a given account or collection of accounts. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Billing/GetBillingHistory/&lt;format&gt; (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Billing.asmx?op=GetBillingHistory


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

  &lt;GetBillingHistory xmlns="http://www.tier3.com/"&gt;

    &lt;request&gt;

       &lt;accountAlias&gt;1000&lt;/accountAlias&gt;

    &lt;/request&gt;

  &lt;/GetBillingHistory&gt;

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
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short name associated with an account.</td>
    </tr>
    <tr>
      <td>OutstandingBalance</td>
      <td>Decimal</td>
      <td>The total unpaid balance associated with the account.</td>
    </tr>
    <tr>
      <td>LedgerEntry</td>
      <td>Complex (see below)</td>
      <td>List of invoices that describe the credits and debits on an account.</td>
    </tr>
  </tbody>
</table>

### LedgerEntry Attributes
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
      <td>InvoiceID</td>
      <td>String</td>
      <td>Identifier for the account's invoice.</td>
    </tr>
    <tr>
      <td>Date</td>
      <td>DateTime</td>
      <td>Date of the invoice.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>Descriptive text of the invoice; typically the name of the invoice.</td>
    </tr>
    <tr>
      <td>Debit</td>
      <td>Decimal</td>
      <td>Charges associated with the invoice period.</td>
    </tr>
    <tr>
      <td>Credit</td>
      <td>Decimal</td>
      <td>Credits applied to the account during this invoice period.</td>
    </tr>
    <tr>
      <td>OutstandingBalance</td>
      <td>Decimal</td>
      <td>Total balance due for this invoice.</td>
    </tr>
  </tbody>
</table>

###Examples
<h4>JSON (REST)</h4>
<pre>{<br />     "AccountAlias":"1001",<br />     "OutstandingBalance":1722.4500,<br />     "BillingHistory":[<br />       {<br />              "InvoiceID":"ID123456",<br />              "Date":"\/Date(1343775600000)\/",<br />              "Description":"Invoice ID123456",<br />              "Debit":1258.8100,<br />              "Credit":0,<br />              "OutstandingBalance":1363.8900,<br />              "ItemID":244,<br />              "DisplayPrecedence":1<br />             },<br />             {<br />              "InvoiceID":"ID67890",<br />              "Date":"\/Date(1346454000000)\/",<br />              "Description":"Invoice ID67890",<br />              "Debit":358.5600,<br />              "Credit":0,<br />              "OutstandingBalance":1722.4500,<br />              "ItemID":277,<br />              "DisplayPrecedence":1<br />       }],<br />     "Success":true,<br />     "Message":"OK",<br />     "StatusCode":0<br />}</pre>

<h4>XML (REST)</h4>
<pre>&lt;BillingHistoryResponse Success="true" Message="OK" StatusCode="0" AccountAlias="RSDA" OutstandingBalance="1722.4500"&gt;

  &lt;BillingHistory&gt;

      &lt;LedgerEntry InvoiceID="ID123456" 

          Date="2012-08-31T23:00:00" 

          Description="Invoice ID123456" 

          Debit="1258.8100" 

          Credit="0" 

          OutstandingBalance="1363.8900" /&gt;

      &lt;LedgerEntry InvoiceID="ID67890" 

          Date="2012-09-30T23:00:00" 

          Description="Invoice ID67890" 

          Debit="358.5600" 

          Credit="0" 

          OutstandingBalance="1722.4500" /&gt;

  &lt;/BillingHistory&gt;

&lt;/BillingHistoryResponse&gt;

  </pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" 

  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

  xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

  &lt;soap:Body&gt;

      &lt;GetBillingHistoryResponse xmlns="http://www.tier3.com/"&gt;

          &lt;GetBillingHistoryResult Success="true" Message="OK" StatusCode="0" AccountAlias="RSDA" OutstandingBalance="1722.4500"&gt;

              &lt;BillingHistory&gt;

                  &lt;LedgerEntry InvoiceID="RSDA4503BF68" 

                      Date="2012-08-31T23:00:00" 

                      Description="Invoice RSDA4503BF68" 

                      Debit="1258.8100" 

                      Credit="0" 

                      OutstandingBalance="1363.8900" /&gt;

                  &lt;LedgerEntry InvoiceID="RSDA9278D23F" 

                      Date="2012-09-30T23:00:00" 

                      Description="Invoice RSDA9278D23F" 

                      Debit="358.5600" Credit="0" 

                      OutstandingBalance="1722.4500" /&gt;

              &lt;/BillingHistory&gt;

          &lt;/GetBillingHistoryResult&gt;

      &lt;/GetBillingHistoryResponse&gt;

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
