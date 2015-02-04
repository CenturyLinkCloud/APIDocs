{{{
  "title": "GetGroupSummaries",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}


Gets the charges for groups and servers within a given account, and for any date range. Calls to this operation must include an authorization cookie acquired from the <a href="/api-docs#authentication-logon">Logon operation.</a>

##URL

    REST: https://api.tier3.com/REST/Billing/GetGroupSummaries/&lt;format&gt; (format = XML | JSON)
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

<h4>JSON (REST)</h4>
<pre>{ <br />    "AccountAlias": "1000",<br />    "StartDate":"2012-11-01",<br />    "EndDate":"2012-11-15"<br />}</pre>

<h4>XML (REST)</h4>
<pre>&lt;BillingRequest&gt;

  &lt;AccountAlias&gt;1000&lt;/AccountAlias&gt;

  &lt;StartDate&gt;2012-11-01&lt;/StartDate&gt;

  &lt;EndDate&gt;2012-11-15&lt;/EndDate&gt;

&lt;/BillingRequest&gt;

</pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

  xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

  xmlns:soap12="http://www.w3.org/2003/05/soap-envelope"&gt;

&lt;soap12:Body&gt;

  &lt;GetGroupSummaries xmlns="http://www.tier3.com/"&gt;

    &lt;accountAlias&gt;1000&lt;/accountAlias&gt;

  &lt;/GetGroupSummaries&gt;

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
<h4>JSON (REST)</h4>
<pre>{<br />     "Summary":<br />     {<br />       "MonthlyEstimate":73.790,<br />       "MonthToDate":73.790,<br />       "CurrentHour":0.0,<br />       "PreviousHour":0.0<br />     },<br />       "AccountAlias":"1000",<br />       "StartDate":"11/1/2012",<br />       "EndDate":"11/15/2012",<br />       "GroupTotals":[<br />       {<br />         "GroupID":1634,<br />         "GroupName":"Group 1",<br />         "LocationAlias":"WA1",<br />         "ServerTotals":[<br />           {<br />           "ServerName":"SERVER1",<br />           "MonthlyEstimate":73.790,<br />           "MonthToDate":73.790,<br />           "CurrentHour":0.0,<br />           "PreviousHour":0.0<br />           }<br />         ],<br />         "MonthlyEstimate":73.790,<br />         "MonthToDate":73.790,<br />         "CurrentHour":0.0,<br />         "PreviousHour":0.0<br />       }],<br />       "Success":true,<br />       "Message":"Ok",<br />       "StatusCode":0<br />}</pre>

<h4>XML (REST)</h4>
<pre>&lt;GroupSummariesResponse Success="true" Message="Ok" StatusCode="0" AccountAlias="1000" StartDate="11/1/2012" EndDate="11/15/2012"&gt;

  &lt;Summary MonthlyEstimate="73.790" MonthToDate="73.790" CurrentHour="0.0" PreviousHour="0.0" /&gt;

  &lt;GroupTotals&gt;

      &lt;ServerGroupTotal MonthlyEstimate="73.790" 

          MonthToDate="73.790" 

          CurrentHour="0.0" 

          PreviousHour="0.0" 

          GroupID="1634" 

          GroupName="Group 1" 

          LocationAlias="WA1"&gt;

          &lt;ServerTotals&gt;

              &lt;ServerTotal MonthlyEstimate="73.790" 

                  MonthToDate="73.790" 

                  CurrentHour="0.0" 

                  PreviousHour="0.0" 

                  ServerName="SERVER1" /&gt;

          &lt;/ServerTotals&gt;

      &lt;/ServerGroupTotal&gt;

  &lt;/GroupTotals&gt;

&lt;/GroupSummariesResponse&gt;

</pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" 

  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

  xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

  &lt;soap:Body&gt;

      &lt;GetGroupSummariesResponse xmlns="http://www.tier3.com/"&gt;

          &lt;GetGroupSummariesResult Success="true" 

              Message="Ok" 

              StatusCode="0" 

              AccountAlias="1000" 

              StartDate="11/1/2012" 

              EndDate="11/16/2012"&gt;

              &lt;Summary MonthlyEstimate="83.180" 

                  MonthToDate="83.180" 

                  CurrentHour="0.223600" 

                  PreviousHour="0.223600" /&gt;

              &lt;GroupTotals&gt;

                  &lt;ServerGroupTotal MonthlyEstimate="83.180" 

                      MonthToDate="83.180" 

                      CurrentHour="0.223600" 

                      PreviousHour="0.223600" 

                      GroupID="1634" 

                      GroupName="Group 1 

                      LocationAlias="WA1"&gt;

                      &lt;ServerTotals&gt;

                          &lt;ServerTotal MonthlyEstimate="83.180" 

                              MonthToDate="83.180" 

                              CurrentHour="0.223600" 

                              PreviousHour="0.223600" 

                              ServerName="SERVER1" /&gt;

                      &lt;/ServerTotals&gt;

                  &lt;/ServerGroupTotal&gt;

              &lt;/GroupTotals&gt;

          &lt;/GetGroupSummariesResult&gt;

      &lt;/GetGroupSummariesResponse&gt;

  &lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;

</pre>

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
