{{{
  "title": "GetGroupSummaries",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}


Gets the charges for groups and servers within a given account, and for any date range. Calls to this operation must include an authorization cookie acquired from the <a href="/api-docs#authentication-logon">Logon operation.</a>

##URL

    REST: https://api.tier3.com/REST/Billing/GetGroupSummaries/<format> (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Billing.asmx?op=GetGroupSummaries

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
      <td>StartDate</td>
      <td>String</td>
      <td>Start date for query range. If missing, this defaults to beginning of the current month.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>EndDate</td>
      <td>String</td>
      <td>End date for query range. If missing, this defaults to current day of the current month.</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

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
      <td>Account that this group summary applied to.</td>
    </tr>
    <tr>
      <td>StartDate</td>
      <td>String</td>
      <td>Start date of the query range.</td>
    </tr>
    <tr>
      <td>EndDate</td>
      <td>Decimal</td>
      <td>End date of the query range.</td>
    </tr>
    <tr>
      <td>Summary</td>
      <td>Complex (see below)</td>
      <td>Overview of costs for the group.</td>
    </tr>
    <tr>
      <td>ServerGroupTotals</td>
      <td>Complex (see below)</td>
      <td>Details of individual costs of the group.</td>
    </tr>
  </tbody>
</table>

### Summary Attributes

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
      <td>MonthlyEstimate</td>
      <td>Decimal</td>
      <td>Estimated costs for all groups based on current usage.</td>
    </tr>
    <tr>
      <td>MonthToDate</td>
      <td>Decimal</td>
      <td>Current charges so far this month.</td>
    </tr>
    <tr>
      <td>CurrentHour</td>
      <td>Decimal</td>
      <td>Charges for the current hour.</td>
    </tr>
    <tr>
      <td>MonthToDate</td>
      <td>Decimal</td>
      <td>Charges for the previous hour.</td>
    </tr>
  </tbody>
</table>

### ServerGroupTotals Attributes

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
      <td>MonthlyEstimate</td>
      <td>Decimal</td>
      <td>Estimated costs for all groups based on current usage.</td>
    </tr>
    <tr>
      <td>MonthToDate</td>
      <td>Decimal</td>
      <td>Current charges so far this month.</td>
    </tr>
    <tr>
      <td>CurrentHour</td>
      <td>Decimal</td>
      <td>Charges for the current hour.</td>
    </tr>
    <tr>
      <td>PreviousHour</td>
      <td>Decimal</td>
      <td>Charges for the previous hour.</td>
    </tr>
    <tr>
      <td>GroupID</td>
      <td>Integer</td>
      <td>Unique identifier for this specific group.</td>
    </tr>
    <tr>
      <td>GroupName</td>
      <td>String</td>
      <td>User-given name to this group.</td>
    </tr>
    <tr>
      <td>LocationAlias</td>
      <td>String</td>
      <td>Data center alias corresponding to this group.</td>
    </tr>
    <tr>
      <td>ServerTotal</td>
      <td>Complex (see below)</td>
      <td>Collection of servers that make up the group, and the individual cost of each.</td>
    </tr>
  </tbody>
</table>

### ServerTotal Attributes

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
      <td>MonthlyEstimate</td>
      <td>Decimal</td>
      <td>Estimated costs for the server based on current usage.</td>
    </tr>
    <tr>
      <td>MonthToDate</td>
      <td>Decimal</td>
      <td>Current charges so far this month.</td>
    </tr>
    <tr>
      <td>CurrentHour</td>
      <td>Decimal</td>
      <td>Charges for the current hour.</td>
    </tr>
    <tr>
      <td>PreviousHour</td>
      <td>Decimal</td>
      <td>Charges for the previous hour.</td>
    </tr>
    <tr>
      <td>ServerName</td>
      <td>String</td>
      <td>Name of this server that is incurring charges.</td>
    </tr>
  </tbody>
</table>

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
      <td>Invalid Start Date. &nbsp;You must provide a valid start date when calling this method.</td>
    </tr>
    <tr>
      <td>1802</td>
      <td>Invalid End Date. &nbsp;You must provide a valid end date when calling this method.</td>
    </tr>
  </tbody>
</table>
