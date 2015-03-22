{{{
  "title": "GetServerHourlyCharges",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the server-based hourly cost for any time period. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/Billing/GetServerHourlyCharges/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Billing.asmx?op=GetServerHourlyCharges

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | Short code for a particular account. If not provided, then the API user's account is used. | No |
| ServerName | String | Name given to the server. | Yes |
| StartDate | DateTime | Start of the query period. | No |
| EndDate | String | End of the query period. | No |

### Examples

#### JSON (REST)

    {
      "AccountAlias": "1000",
      "ServerName":"QA1RSDASER101",
      "StartDate":"2012-11-14",
      "EndDate":"2012-11-15"
    }

#### XML (REST)

    <ServerRequest>
      <AccountAlias>RSDA</AccountAlias>
      <ServerName>QA1RSDASER101</ServerName>
      <StartDate>2012-11-14</StartDate>
      <EndDate>2012-11-15</EndDate>
    </ServerRequest>

#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema"
      xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
        <soap12:Body>
            <GetServerHourlyCharges xmlns="http://www.tier3.com/">
                <accountAlias>1000</accountAlias>
                <name>QA1RSDASER101</name>
                <startDate>2012-11-15</startDate>
                <endDate>2012-11-15</endDate>
            </GetServerHourlyCharges>
        </soap12:Body>
    </soap12:Envelope>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| AccountAlias | String | Short code for a particular account. |
| ServerName | String | Name given to the server. |
| StartDate | DateTime | Start of the query period. |
| EndDate | DateTime | End of the query period. |
| Summary | Complex | Aggregation of charges for the server. |
| HourlyCharges | Complex | Per hour for the server. |

### Examples

#### JSON (REST)

    {
      "Summary":
        {
          "MonthlyEstimate":0.0,
          "MonthToDate":0.0,
          "CurrentHour":0.0,
          "PreviousHour":0.0
        },
      "AccountAlias":"RSDA",
      "ServerName":"QA1RSDASER101",
      "StartDate":"\/Date(1352851200000)\/",
      "EndDate":"\/Date(1352937600000)\/",
      "HourlyCharges": [
        {
          "Hour":"2012-11-14T12:00:00",
          "ProcessorCost":"0",
          "MemoryCost":"0",
          "StorageCost":"0",
          "OSCost":"0"
        },
        {
          "Hour":"2012-11-14T01:00:00",
          "ProcessorCost":"0",
          "MemoryCost":"0",
          "StorageCost":"0",
          "OSCost":"0"
        }
      ],
      "Success":true,
      "Message":"OK",
      "StatusCode":0
    }

#### XML (REST)

    <ServerHourlyChargesResponse
      Success="true"
      Message="OK"
      StatusCode="0"
      AccountAlias="RSDA"
      ServerName="QA1RSDASER101"
      StartDate="2012-11-14T00:00:00"
      EndDate="2012-11-15T00:00:00">
        <Summary MonthlyEstimate="0.0" MonthToDate="0.0" CurrentHour="0.0" PreviousHour="0.0" />
        <HourlyCharge>
            <ServerHourlyCost Hour="2012-11-14T12:00:00" ProcessorCost="0" MemoryCost="0" StorageCost="0" OSCost="0" />
            <ServerHourlyCost Hour="2012-11-14T01:00:00" ProcessorCost="0" MemoryCost="0" StorageCost="0" OSCost="0" />
        </HourlyCharge>
    </ServerHourlyChargesResponse>

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema">
        <soap:Body>
            <GetServerHourlyChargesResponse xmlns="http://www.tier3.com/">
                <GetServerHourlyChargesResult Success="true"
                  Message="OK"
                  StatusCode="0"
                  AccountAlias="RSDA"
                  ServerName="QA1RSDASER101"
                  StartDate="2012-11-14T00:00:00"
                  EndDate="2012-11-15T00:00:00">
                    <Summary MonthlyEstimate="0.0" MonthToDate="0.0" CurrentHour="0.0" PreviousHour="0.0" />
                    <HourlyCharges>
                        <ServerHourlyCost Hour="2012-11-14T12:00:00" ProcessorCost="0" MemoryCost="0" StorageCost="0" OSCost="0" />
                        <ServerHourlyCost Hour="2012-11-14T01:00:00" ProcessorCost="0" MemoryCost="0" StorageCost="0" OSCost="0" />
                    </HourlyCharges>
                </GetServerHourlyChargesResult>
            </GetServerHourlyChargesResponse>
        </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 5 | Resource Does Not Exist.  You must provide a valid server identifier when calling this method. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 541 | Hardware Group Not Found.  You must provide a valid hardware group ID when calling this method. |
| 1800 | Account Not Found.  You must provide a valid account alias when calling this method. |
| 1801 | Start Date Invalid.  You must provide a valid start date when calling this method. |
| 1802 | End Date Invalid.  You must provide a valid end date when calling this method. |
