{{{
  "title": "GetGroupSummaries",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}


Gets the charges for groups and servers within a given account, and for any date range. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

##URL

    REST: https://api.ctl.io/REST/Billing/GetGroupSummaries/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Billing.asmx?op=GetGroupSummaries

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | Short code for a particular account. If not provided, then the API user's account is used. | No |
| StartDate | String | Start date for query range. If missing, this defaults to beginning of the current month. | No |
| EndDate | String | End date for query range. If missing, this defaults to current day of the current month. | No |

### Examples

#### JSON (REST)

    {
      "AccountAlias": "1000",
      "StartDate":"2012-11-01",
      "EndDate":"2012-11-15"
    }

#### XML (REST)

    <BillingRequest>
      <AccountAlias>1000</AccountAlias>
      <StartDate>2012-11-01</StartDate>
      <EndDate>2012-11-15</EndDate>
    </BillingRequest>

#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema"
      xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
        <soap12:Body>
            <GetGroupSummaries xmlns="http://www.tier3.com/">
                <accountAlias>1000</accountAlias>
            </GetGroupSummaries>
        </soap12:Body>
    </soap12:Envelope>  

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| AccountAlias | String | Account that this group summary applied to. |
| StartDate | String | Start date of the query range. |
| EndDate | Decimal | End date of the query range. |
| Summary | Complex (see below) | Overview of costs for the group. |
| ServerGroupTotals | Complex (see below) | Details of individual costs of the group. |

### Summary Attributes

| Name | Type | Description |
| --- | --- | --- |
| MonthlyEstimate | Decimal | Estimated costs for all groups based on current usage. |
| MonthToDate | Decimal | Current charges so far this month. |
| CurrentHour | Decimal | Charges for the current hour. |
| MonthToDate | Decimal | Charges for the previous hour. |

### ServerGroupTotals Attributes

| Name | Type | Description |
| --- | --- | --- |
| MonthlyEstimate | Decimal | Estimated costs for all groups based on current usage. |
| MonthToDate | Decimal | Current charges so far this month. |
| CurrentHour | Decimal | Charges for the current hour. |
| PreviousHour | Decimal | Charges for the previous hour. |
| GroupID | Integer | Unique identifier for this specific group. |
| GroupName | String | User-given name to this group. |
| LocationAlias | String | Data center alias corresponding to this group. |
| ServerTotal | Complex (see below) | Collection of servers that make up the group, and the individual cost of each. |

### ServerTotal Attributes

| Name | Type | Description |
| --- | --- | --- |
| MonthlyEstimate | Decimal | Estimated costs for the server based on current usage. |
| MonthToDate | Decimal | Current charges so far this month. |
| CurrentHour | Decimal | Charges for the current hour. |
| PreviousHour | Decimal | Charges for the previous hour. |
| ServerName | String | Name of this server that is incurring charges. |

### Examples

#### JSON (REST)

    {
      "Summary": {
          "MonthlyEstimate":73.790,
          "MonthToDate":73.790,
          "CurrentHour":0.0,
          "PreviousHour":0.0
      },
      "AccountAlias":"1000",
      "StartDate":"11/1/2012",
      "EndDate":"11/15/2012",
      "GroupTotals": [
        {
          "GroupID":1634,
          "GroupName":"Group 1",
          "LocationAlias":"WA1",
          "ServerTotals":[
            {
              "ServerName":"SERVER1",
              "MonthlyEstimate":73.790,
              "MonthToDate":73.790,
              "CurrentHour":0.0,
              "PreviousHour":0.0
            }
          ],
          "MonthlyEstimate":73.790,
          "MonthToDate":73.790,
          "CurrentHour":0.0,
          "PreviousHour":0.0
        }
      ],
      "Success":true,
      "Message":"Ok",
      "StatusCode":0
    }

#### XML (REST)

    <GroupSummariesResponse Success="true" Message="Ok" StatusCode="0" AccountAlias="1000" StartDate="11/1/2012" EndDate="11/15/2012">
        <Summary MonthlyEstimate="73.790" MonthToDate="73.790" CurrentHour="0.0" PreviousHour="0.0" />
        <GroupTotals>
            <ServerGroupTotal MonthlyEstimate="73.790"
                MonthToDate="73.790"
                CurrentHour="0.0"
                PreviousHour="0.0"
                GroupID="1634"
                GroupName="Group 1"
                LocationAlias="WA1">
                <ServerTotals>
                    <ServerTotal MonthlyEstimate="73.790"
                        MonthToDate="73.790"
                        CurrentHour="0.0"
                        PreviousHour="0.0"
                        ServerName="SERVER1" />
                </ServerTotals>
            </ServerGroupTotal>
        </GroupTotals>
    </GroupSummariesResponse>

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema">
        <soap:Body>
            <GetGroupSummariesResponse xmlns="http://www.tier3.com/">
                <GetGroupSummariesResult Success="true"
                  Message="Ok"
                  StatusCode="0"
                  AccountAlias="1000"
                  StartDate="11/1/2012"
                  EndDate="11/16/2012">
                    <Summary MonthlyEstimate="83.180"
                        MonthToDate="83.180"
                        CurrentHour="0.223600"
                        PreviousHour="0.223600" />
                    <GroupTotals>
                        <ServerGroupTotal MonthlyEstimate="83.180"
                          MonthToDate="83.180"
                          CurrentHour="0.223600"
                          PreviousHour="0.223600"
                          GroupID="1634"
                          GroupName="Group 1
                          LocationAlias="WA1">
                            <ServerTotals>
                                <ServerTotal MonthlyEstimate="83.180"
                                  MonthToDate="83.180"
                                  CurrentHour="0.223600"
                                  PreviousHour="0.223600"
                                  ServerName="SERVER1" />
                            </ServerTotals>
                        </ServerGroupTotal>
                    </GroupTotals>
                </GetGroupSummariesResult>
            </GetGroupSummariesResponse>
        </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 541 | Hardware Group Not Found.  You must provide a valid hardware group ID when calling this method. |
| 1800 | Account Not Found.  You must provide a valid account alias when calling this method. |
| 1801 | Invalid Start Date.  You must provide a valid start date when calling this method. |
| 1802 | Invalid End Date.  You must provide a valid end date when calling this method. |
