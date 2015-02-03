{{{
  "title": "GetInvoiceDetails",
  "date": "11-19-2013",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the details for a given invoice within an account. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Billing/GetInvoiceDetails/&lt;format&gt; (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Billing.asmx?op=GetInvoiceDetails

## Request
###Attributes
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
      <td>Yes</td>
    </tr>
    <tr>
      <td>InvoiceID</td>
      <td>String</td>
      <td>Unique identifier for a given invoice.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON (REST)</h4>
<pre>{ <br />    "AccountAlias": "1000",<br />    "InvoiceID":"ABC1235"<br />}</pre>

<h4>XML (REST)</h4>
<pre>&lt;InvoiceRequest&gt;

  &lt;AccountAlias&gt;1000&lt;/AccountAlias&gt;

  &lt;InvoiceID&gt;ABC1235&lt;/InvoiceID&gt;

&lt;/InvoiceRequest&gt;

  </pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

  xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

  xmlns:soap12="http://www.w3.org/2003/05/soap-envelope"&gt;

&lt;soap12:Body&gt;

  &lt;GetInvoiceDetails xmlns="http://www.tier3.com/"&gt;

    &lt;accountAlias&gt;1000&lt;/accountAlias&gt;

    &lt;invoiceId&gt;ABC1235&lt;/invoiceId&gt;

  &lt;/GetInvoiceDetails &gt;

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
      <td>OpeningBalance</td>
      <td>Decimal</td>
      <td>Previous balance on the account.</td>
    </tr>
    <tr>
      <td>NewCharges</td>
      <td>Decimal</td>
      <td>New charges for the invoice period.</td>
    </tr>
    <tr>
      <td>Payments</td>
      <td>Decimal</td>
      <td>Amount of payments received.</td>
    </tr>
    <tr>
      <td>EndingBalance</td>
      <td>Decimal</td>
      <td>Total billed amount for this invoice.</td>
    </tr>
    <tr>
      <td>CurrentOutstandingBalance</td>
      <td>Decimal</td>
      <td>Total amount owed by this account.</td>
    </tr>
    <tr>
      <td>Invoice</td>
      <td>Complex (see below)</td>
      <td>Invoice details and line items.</td>
    </tr>
  </tbody>
</table>

### Invoice Attributes
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
      <td>ID</td>
      <td>String</td>
      <td>Unique identifier of the invoice.</td>
    </tr>
    <tr>
      <td>Terms</td>
      <td>String</td>
      <td>Billing terms of this invoice.</td>
    </tr>
    <tr>
      <td>CompanyName</td>
      <td>String</td>
      <td>Name of the company associated with the account.</td>
    </tr>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short code of the account.</td>
    </tr>
    <tr>
      <td>Address1</td>
      <td>String</td>
      <td>Street address associated with the account.</td>
    </tr>
    <tr>
      <td>City</td>
      <td>String</td>
      <td>City associated with the account.</td>
    </tr>
    <tr>
      <td>StateProvince</td>
      <td>String</td>
      <td>State or province associated with the account.</td>
    </tr>
    <tr>
      <td>PostalCode</td>
      <td>String</td>
      <td>Postcal code associated with the account.</td>
    </tr>
    <tr>
      <td>BillingContactEmail</td>
      <td>String</td>
      <td>Email address associated with the account.</td>
    </tr>
    <tr>
      <td>InvoiceCCEmail</td>
      <td>String</td>
      <td>Secondary email address associated with the account.</td>
    </tr>
    <tr>
      <td>TotalAmount</td>
      <td>Decimal</td>
      <td>Total amount of this invoice.</td>
    </tr>
    <tr>
      <td>InvoiceDate</td>
      <td>DateTime</td>
      <td>Date of the invoice.</td>
    </tr>
    <tr>
      <td>PONumber</td>
      <td>String</td>
      <td>Purchase Order identifier.</td>
    </tr>
    <tr>
      <td>InvoiceLineItem</td>
      <td>Complex (see below)</td>
      <td>Individual line item on the invoice.</td>
    </tr>
  </tbody>
</table>

### InvoiceLineItem Attributes
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
      <td>Quantity</td>
      <td>Integer</td>
      <td>Count of the item that is being charged.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>Typically the name of the billed resource or container.</td>
    </tr>
    <tr>
      <td>UnitCost</td>
      <td>Decimal</td>
      <td>Cost of one unit of the resource.</td>
    </tr>
    <tr>
      <td>ItemTotal</td>
      <td>Decimal</td>
      <td>Unit cost multiplied by the quantity.</td>
    </tr>
    <tr>
      <td>ServiceLocation</td>
      <td>String</td>
      <td>Data center alias associated with this resource.</td>
    </tr>
    <tr>
      <td>LineItemDetail</td>
      <td>Complex (see below)</td>
      <td>Individual line item description and cost. For instance, may refer to the servers within a group.</td>
    </tr>
  </tbody>
</table>

### LineItemDetail Attributes
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
      <td>Description</td>
      <td>String</td>
      <td>Typically the name of the lowest level billed resource, such as a server name.</td>
    </tr>
    <tr>
      <td>Cost</td>
      <td>Decimal</td>
      <td>Cost of this resource.</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON (REST)</h4>
<pre>{

   "OpeningBalance":1363.8900,

   "NewCharges":358.5600,

   "Payments":0.0,

   "EndingBalance":1722.4500,

   "CurrentOutstandingBalance":1722.4500,

   "Invoice":

      {

      "ID":"RSDA9278D23F",

      "Terms":"Upon Receipt",

      "CompanyName":"Demo Account",

      "AccountAlias":"1000",

      "ParentAccountAlias":null,

      "Address1":"123 100th St NE",

      "Address2":null,

      "City":"Bellevue",

      "StateProvince":"WA",

      "PostalCode":"98155",

      "BillingContactEmail":"user@company.com",

      "InvoiceCCEmail":"",

      "TotalAmount":358.5600,

      "InvoiceDate":"\/Date(1349046000000)\/",

      "PONumber":null,

      "LineItems":[

         {

            "Quantity":1,

            "Description":"Group 1",

            "UnitCost":103.5800,

            "ItemTotal":103.5800,

            "ServiceLocation":"WA1",

            "ItemDetails":[

              {

                  "Description":"SERVER123",

                  "Cost":103.5800

              }]

          },

          {

              "Quantity":1,

              "Description":"Demo Group 2",

              "UnitCost":252.9800,

              "ItemTotal":252.9800,

              "ServiceLocation":"WA1",

              "ItemDetails":[

                {

                    "Description":"SERVER987",

                    "Cost":252.9800

                }]

            },

            {

                "Quantity":1,

                "Description":"External IP Address (QA1)",

                "UnitCost":2.0000,

                "ItemTotal":2.0000,

                "ServiceLocation":"WA1",

                "ItemDetails":[]

             }

         ]},

         "Success":true,

         "Message":"Ok",

         "StatusCode":0

}</pre>

<h4>XML (REST)</h4>
<pre>&lt;InvoiceDetailResponse 

  Success="true" 

  Message="Ok" 

  StatusCode="0" 

  OpeningBalance="1363.8900" 

  NewCharges="358.5600" 

  Payments="0.0" 

  EndingBalance="1722.4500" 

  CurrentOutstandingBalance="1722.4500"&gt;

  &lt;Invoice 

      ID="RSDA9278D23F" 

      Terms="Upon Receipt" 

      CompanyName="Demo Company" 

      AccountAlias="1000" 

      Address1="123 100th St NE" 

      City="Bellevue" 

      StateProvince="WA" 

      PostalCode="98155" 

      BillingContactEmail="user@company.com" 

      InvoiceCCEmail="" 

      TotalAmount="358.5600" 

      InvoiceDate="2012-09-30T23:00:00"&gt;

      &lt;LineItems&gt;

          &lt;InvoiceLineItem Quantity="1" Description="Demo Group 1" UnitCost="103.5800" ItemTotal="103.5800" ServiceLocation="WA1"&gt;

              &lt;ItemDetails&gt;

                  &lt;LineItemDetail Description="SERVER123" Cost="103.5800" /&gt;

              &lt;/ItemDetails&gt;

          &lt;/InvoiceLineItem&gt;

          &lt;InvoiceLineItem Quantity="1" Description="Demo Group 2" UnitCost="252.9800" ItemTotal="252.9800" ServiceLocation="WA1"&gt;

              &lt;ItemDetails&gt;

                  &lt;LineItemDetail Description="SERVER987" Cost="252.9800" /&gt;

              &lt;/ItemDetails&gt;

          &lt;/InvoiceLineItem&gt;

          &lt;InvoiceLineItem Quantity="1" Description="External IP Address (QA1)" UnitCost="2.0000" ItemTotal="2.0000" ServiceLocation="QA1"&gt;

              &lt;ItemDetails /&gt;

          &lt;/InvoiceLineItem&gt;

      &lt;/LineItems&gt;

  &lt;/Invoice&gt;

&lt;/InvoiceDetailResponse&gt;

</pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" 

  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

  xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

  &lt;soap:Body&gt;

      &lt;GetInvoiceDetailsResponse xmlns="http://www.tier3.com/"&gt;

          &lt;GetInvoiceDetailsResult 

              Success="true" 

              Message="Ok" 

              StatusCode="0" 

              OpeningBalance="1363.8900" 

              NewCharges="358.5600" 

              Payments="0.0" 

              EndingBalance="1722.4500" 

              CurrentOutstandingBalance="1722.4500"&gt;

              &lt;Invoice ID="RSDA9278D23F" 

                  Terms="Upon Receipt" 

                  CompanyName="Demo Account" 

                  AccountAlias="1000" 

                  Address1="123 100th St NE" 

                  City="Bellevue" 

                  StateProvince="WA" 

                  PostalCode="98155" 

                  BillingContactEmail="user@company.com" 

                  InvoiceCCEmail="" 

                  TotalAmount="358.5600" 

                  InvoiceDate="2012-09-30T23:00:00"&gt;

                  &lt;LineItems&gt;

                      &lt;InvoiceLineItem Quantity="1" Description="Group 1" UnitCost="103.5800" ItemTotal="103.5800" ServiceLocation="WA1"&gt;

                          &lt;ItemDetails&gt;

                              &lt;LineItemDetail Description="SERVER123" Cost="103.5800" /&gt;&lt;/ItemDetails&gt;

                      &lt;/InvoiceLineItem&gt;

                      &lt;InvoiceLineItem Quantity="1" Description="Group 2" UnitCost="252.9800" ItemTotal="252.9800" ServiceLocation="WA1"&gt;

                          &lt;ItemDetails&gt;&lt;LineItemDetail Description="SERVER987" Cost="252.9800" /&gt;&lt;/ItemDetails&gt;

                          &lt;/InvoiceLineItem&gt;

                      &lt;InvoiceLineItem Quantity="1" Description="External IP Address (QA1)" UnitCost="2.0000" ItemTotal="2.0000" ServiceLocation="WA1"&gt;

                          &lt;ItemDetails /&gt;

                      &lt;/InvoiceLineItem&gt;

                  &lt;/LineItems&gt;

              &lt;/Invoice&gt;

          &lt;/GetInvoiceDetailsResult&gt;

      &lt;/GetInvoiceDetailsResponse&gt;

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
    <tr>
      <td>1804</td>
      <td>Invoice ID Required. &nbsp;You must provide a valid invoice ID when calling this method.</td>
    </tr>
    <tr>
      <td>1805</td>
      <td>Invoice Not Found. &nbsp;There is no valid invoice for the ID provided.</td>
    </tr>
  </tbody>
</table>
