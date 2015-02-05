{{{
  "title": "GetServerHourlyCharges",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the server-based hourly cost for any time period. Calls to this operation must include an authorization cookie acquired from the <a href="/api-docs#authentication-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Billing/GetServerHourlyCharges/<format> (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Billing.asmx?op=GetServerHourlyCharges

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
      <td>Short code for a particular account. If not provided, then the API user's account is used.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>ServerName</td>
      <td>String</td>
      <td>Name given to the server.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>StartDate</td>
      <td>DateTime</td>
      <td>Start of the query period.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>EndDate</td>
      <td>String</td>
      <td>End of the query period.</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

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
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short code for a particular account.</td>
    </tr>
    <tr>
      <td>ServerName</td>
      <td>String</td>
      <td>Name given to the server.</td>
    </tr>
    <tr>
      <td>StartDate</td>
      <td>DateTime</td>
      <td>Start of the query period.</td>
    </tr>
    <tr>
      <td>EndDate</td>
      <td>DateTime</td>
      <td>End of the query period.</td>
    </tr>
    <tr>
      <td>Summary</td>
      <td>Complex</td>
      <td>Aggregation of charges for the server.</td>
    </tr>
    <tr>
      <td>HourlyCharges</td>
      <td>Complex</td>
      <td>Per hour for the server.</td>
    </tr>
  </tbody>
</table>

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

      "HourlyCharges":[

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
    <tr>
      <td>1801</td>
      <td>Start Date Invalid. &nbsp;You must provide a valid start date when calling this method.</td>
    </tr>
    <tr>
      <td>1802</td>
      <td>End Date Invalid. &nbsp;You must provide a valid end date when calling this method.</td>
    </tr>
  </tbody>
</table>
