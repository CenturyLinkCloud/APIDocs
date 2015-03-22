{{{
  "title": "GetGroupEstimate",
  "date": "5-6-2013",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets estimated costs for a group of servers. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/Billing/GetGroupEstimate/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Billing.asmx?op=GetGroupEstimate

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | Short code for a particular account. If not provided, then the API user's account is used. | No |
| HardwareGroupID | Integer | Unique identifier of the group that can be acquired via Groups API, or by retrieving this value from the URL when viewing the group in the Control Portal. | Yes |

### Examples

#### JSON (REST)

    {
      "AccountAlias": "1000",
      "HardwareGroupID":"5000"
    }

#### XML (REST)

    <GroupEstimateRequest>
      <AccountAlias>1000</AccountAlias>
      <HardwareGroupID>5000</HardwareGroupID>
    </GroupEstimateRequest>

#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema"
      xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
        <soap12:Body>
            <GetGroupEstimate xmlns="http://www.tier3.com/">
                <groupId>5000</groupId>
            </GetGroupEstimate>
        </soap12:Body>
    </soap12:Envelope>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| MonthlyEstimate | Decimal | Estimated cost of this group given current rate of usage. |
| MonthToDate | Decimal | Charges incurred up to today. |
| CurrentHour | Decimal | Charges for the current hour of usage. |
| PreviousHour | Decimal | Charges for the previous hour of usage. |

### Examples

#### JSON (REST)

    {
      "MonthlyEstimate":0,
      "MonthToDate":0,
      "CurrentHour":0,
      "PreviousHour":0,
      "Success":true,
      "Message":"OK",
      "StatusCode":0
    }

#### XML (REST)

    <BillingResponse Success="true"
      Message="OK"
      StatusCode="0"
      MonthlyEstimate="0"
      MonthToDate="0"
      CurrentHour="0"
      PreviousHour="0" />

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema">
        <soap:Body>
            <GetGroupEstimateResponse xmlns="http://www.tier3.com/">
                <GetGroupEstimateResult Success="true"
                    Message="OK"
                    StatusCode="0"
                    MonthlyEstimate="0"
                    MonthToDate="0" 
                    CurrentHour="0"
                    PreviousHour="0" />
            </GetGroupEstimateResponse>
        </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 541 | Hardware Group Not Found.  You must provide a valid hardware group ID when calling this method. |
| 1800 | Account Not Found.  You must provide a valid account alias when calling this method. |
