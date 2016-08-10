{{{
  "title": "GetInvoiceDetails",
  "date": "11-19-2013",
  "author": "Richard Seroter",
  "attachments": []
}}}

## V2 API AVAILABLE

Please note that there is an equivalent V2 API. Please use the V2 Billing | [Get Invoice Data for an Account Alias](../v2/#billing-get-invoice-data-for-an-account-alias) API.

Gets the details for a given invoice within an account. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/Billing/GetInvoiceDetails/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Billing.asmx?op=GetInvoiceDetails

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | Short code for a particular account. If not provided, then the API user's account is used. | Yes |
| InvoiceID | String | Unique identifier for a given invoice. | Yes |

### Examples

#### JSON (REST)

    {
      "AccountAlias": "1000",
      "InvoiceID":"ABC1235"
    }

#### XML (REST)

    <InvoiceRequest>
      <AccountAlias>1000</AccountAlias>
      <InvoiceID>ABC1235</InvoiceID>
    </InvoiceRequest>

#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema"
      xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
        <soap12:Body>
            <GetInvoiceDetails xmlns="http://www.tier3.com/">
                <accountAlias>1000</accountAlias>
                <invoiceId>ABC1235</invoiceId>
            </GetInvoiceDetails >
        </soap12:Body>
    </soap12:Envelope>  

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| OpeningBalance | Decimal | Previous balance on the account. |
| NewCharges | Decimal | New charges for the invoice period. |
| Payments | Decimal | Amount of payments received. |
| EndingBalance | Decimal | Total billed amount for this invoice. |
| CurrentOutstandingBalance | Decimal | Total amount owed by this account. |
| Invoice | Complex (see below) | Invoice details and line items. |
| SupportLevel | String | Indicator of support level for the account.<br/>developer,<br/>legacy,<br/>professional,<br/>enterprise |

### Invoice Attributes

| Name | Type | Description |
| --- | --- | --- |
| ID | String | Unique identifier of the invoice. |
| Terms | String | Billing terms of this invoice. |
| CompanyName | String | Name of the company associated with the account. |
| AccountAlias | String | Short code of the account. |
| Address1 | String | Street address associated with the account. |
| City | String | City associated with the account. |
| StateProvince | String | State or province associated with the account. |
| PostalCode | String | Postcal code associated with the account. |
| BillingContactEmail | String | Email address associated with the account. |
| InvoiceCCEmail | String | Secondary email address associated with the account. |
| TotalAmount | Decimal | Total amount of this invoice. |
| InvoiceDate | DateTime | Date of the invoice. |
| PONumber | String | Purchase Order identifier. |
| InvoiceLineItem | Complex (see below) | Individual line item on the invoice. |

### InvoiceLineItem Attributes

| Name | Type | Description |
| --- | --- | --- |
| Quantity | Integer | Count of the item that is being charged. |
| Description | String | Typically the name of the billed resource or container. |
| UnitCost | Decimal | Cost of one unit of the resource. |
| ItemTotal | Decimal | Unit cost multiplied by the quantity. |
| ServiceLocation | String | Data center alias associated with this resource. |
| LineItemDetail | Complex (see below) | Individual line item description and cost. For instance, may refer to the servers within a group. |

### LineItemDetail Attributes

| Name | Type | Description |
| --- | --- | --- |
| Description | String | Typically the name of the lowest level billed resource, such as a server name. |
| Cost | Decimal | Cost of this resource. |

### Examples

#### JSON (REST)

    {
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
                }
              ]
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
                }
              ]
            },
            {
              "Quantity":1,
              "Description":"External IP Address (QA1)",
              "UnitCost":2.0000,
              "ItemTotal":2.0000,
              "ServiceLocation":"WA1",
              "ItemDetails":[]
            }
          ]
        },
      "Success":true,
      "Message":"Ok",
      "StatusCode":0
    }

#### XML (REST)

    <InvoiceDetailResponse
      Success="true"
      Message="Ok"
      StatusCode="0"
      OpeningBalance="1363.8900"
      NewCharges="358.5600"
      Payments="0.0"
      EndingBalance="1722.4500"
      CurrentOutstandingBalance="1722.4500">
      <Invoice
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
        InvoiceDate="2012-09-30T23:00:00">
          <LineItems>
              <InvoiceLineItem Quantity="1" Description="Demo Group 1" UnitCost="103.5800" ItemTotal="103.5800" ServiceLocation="WA1">
                  <ItemDetails>
                      <LineItemDetail Description="SERVER123" Cost="103.5800" />
                  </ItemDetails>
              </InvoiceLineItem>
              <InvoiceLineItem Quantity="1" Description="Demo Group 2" UnitCost="252.9800" ItemTotal="252.9800" ServiceLocation="WA1">
                  <ItemDetails>
                      <LineItemDetail Description="SERVER987" Cost="252.9800" />
                  </ItemDetails>
              </InvoiceLineItem>
              <InvoiceLineItem Quantity="1" Description="External IP Address (QA1)" UnitCost="2.0000" ItemTotal="2.0000" ServiceLocation="QA1">
                  <ItemDetails />
              </InvoiceLineItem>
          </LineItems>
      </Invoice>
    </InvoiceDetailResponse>

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema">
        <soap:Body>
            <GetInvoiceDetailsResponse xmlns="http://www.tier3.com/">
                <GetInvoiceDetailsResult
                  Success="true"
                  Message="Ok"
                  StatusCode="0"
                  OpeningBalance="1363.8900"
                  NewCharges="358.5600"
                  Payments="0.0"
                  EndingBalance="1722.4500"
                  CurrentOutstandingBalance="1722.4500">
                    <Invoice ID="RSDA9278D23F"
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
                      InvoiceDate="2012-09-30T23:00:00">
                        <LineItems>
                            <InvoiceLineItem Quantity="1" Description="Group 1" UnitCost="103.5800" ItemTotal="103.5800" ServiceLocation="WA1">
                                <ItemDetails>
                                    <LineItemDetail Description="SERVER123" Cost="103.5800" /></ItemDetails>
                            </InvoiceLineItem>
                            <InvoiceLineItem Quantity="1" Description="Group 2" UnitCost="252.9800" ItemTotal="252.9800" ServiceLocation="WA1">
                                <ItemDetails><LineItemDetail Description="SERVER987" Cost="252.9800" /></ItemDetails>
                                </InvoiceLineItem>
                            <InvoiceLineItem Quantity="1" Description="External IP Address (QA1)" UnitCost="2.0000" ItemTotal="2.0000" ServiceLocation="WA1">
                                <ItemDetails />
                            </InvoiceLineItem>
                        </LineItems>
                    </Invoice>
                </GetInvoiceDetailsResult>
            </GetInvoiceDetailsResponse>
        </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1800 | Account Not Found.  You must provide a valid account alias when calling this method. |
| 1804 | Invoice ID Required.  You must provide a valid invoice ID when calling this method. |
| 1805 | Invoice Not Found.  There is no valid invoice for the ID provided. |
