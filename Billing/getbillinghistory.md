{{{
  "title": "GetBillingHistory",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}


Gets the entire billing history for a given account or collection of accounts. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/Billing/GetBillingHistory/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Billing.asmx?op=GetBillingHistory

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
            <GetBillingHistory xmlns="http://www.tier3.com/">
                <request>
                   <accountAlias>1000</accountAlias>
                </request>
            </GetBillingHistory>
        </soap:Body>
    </soap:Envelope>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| AccountAlias | String | Short name associated with an account. |
| OutstandingBalance | Decimal | The total unpaid balance associated with the account. |
| LedgerEntry | Complex (see below) | List of invoices that describe the credits and debits on an account. |

### LedgerEntry Attributes

| Name | Type | Description |
| --- | --- | --- |
| InvoiceID | String | Identifier for the account's invoice. |
| Date | DateTime | Date of the invoice. |
| Description | String | Descriptive text of the invoice; typically the name of the invoice. |
| Debit | Decimal | Charges associated with the invoice period. |
| Credit | Decimal | Credits applied to the account during this invoice period. |
| OutstandingBalance | Decimal | Total balance due for this invoice. |

### Examples

#### JSON (REST)

    {
      "AccountAlias":"1001",
      "OutstandingBalance":1722.4500,
      "BillingHistory":[
        {
         "InvoiceID":"ID123456",
         "Date":"\/Date(1343775600000)\/",
         "Description":"Invoice ID123456",
         "Debit":1258.8100,
         "Credit":0,
         "OutstandingBalance":1363.8900,
         "ItemID":244,
         "DisplayPrecedence":1
        },
        {
        "InvoiceID":"ID67890",
        "Date":"\/Date(1346454000000)\/",
        "Description":"Invoice ID67890",
        "Debit":358.5600,
        "Credit":0,
        "OutstandingBalance":1722.4500,
        "ItemID":277,
        "DisplayPrecedence":1
        }
      ],
      "Success":true,
      "Message":"OK",
      "StatusCode":0
    }

#### XML (REST)

    <BillingHistoryResponse Success="true" Message="OK" StatusCode="0" AccountAlias="RSDA" OutstandingBalance="1722.4500">
        <BillingHistory>
            <LedgerEntry InvoiceID="ID123456"
                Date="2012-08-31T23:00:00"
                Description="Invoice ID123456"
                Debit="1258.8100"
                Credit="0"
                OutstandingBalance="1363.8900" />
            <LedgerEntry InvoiceID="ID67890"
                Date="2012-09-30T23:00:00"
                Description="Invoice ID67890"
                Debit="358.5600"
                Credit="0"
                OutstandingBalance="1722.4500" />
        </BillingHistory>
    </BillingHistoryResponse>


#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema">
        <soap:Body>
            <GetBillingHistoryResponse xmlns="http://www.tier3.com/">
                <GetBillingHistoryResult Success="true" Message="OK" StatusCode="0" AccountAlias="RSDA" OutstandingBalance="1722.4500">
                    <BillingHistory>
                        <LedgerEntry InvoiceID="RSDA4503BF68"
                            Date="2012-08-31T23:00:00"
                            Description="Invoice RSDA4503BF68"
                            Debit="1258.8100"
                            Credit="0"
                            OutstandingBalance="1363.8900" />
                        <LedgerEntry InvoiceID="RSDA9278D23F"
                            Date="2012-09-30T23:00:00"
                            Description="Invoice RSDA9278D23F"
                            Debit="358.5600" Credit="0"
                            OutstandingBalance="1722.4500" />
                    </BillingHistory>
                </GetBillingHistoryResult>
            </GetBillingHistoryResponse>
        </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1800 | Account Not Found.  You must provide a valid account alias when calling this method. |
