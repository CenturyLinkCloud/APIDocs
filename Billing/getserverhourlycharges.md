{{{
  "title": "GetServerHourlyCharges",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets the server-based hourly cost for any time period. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Billing/GetServerHourlyCharges/&lt;format&gt; (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Billing.asmx?op=GetServerHourlyCharges

## Request
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
      <td><strong>Required</strong>
      </td>
    </tr>
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
<h4>JSON (REST)</h4>
<pre>{ <br />    "AccountAlias": "1000",<br />    "ServerName":"QA1RSDASER101",<br />     "StartDate":"2012-11-14",<br />     "EndDate":"2012-11-15"<br />}</pre>

<h4>XML (REST)</h4>
<pre>&lt;ServerRequest&gt;

  &lt;AccountAlias&gt;RSDA&lt;/AccountAlias&gt;

  &lt;ServerName&gt;QA1RSDASER101&lt;/ServerName&gt;

  &lt;StartDate&gt;2012-11-14&lt;/StartDate&gt;

  &lt;EndDate&gt;2012-11-15&lt;/EndDate&gt;

&lt;/ServerRequest&gt;

</pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

  xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

  xmlns:soap12="http://www.w3.org/2003/05/soap-envelope"&gt;

&lt;soap12:Body&gt;

  &lt;GetServerHourlyCharges xmlns="http://www.tier3.com/"&gt;

      &lt;accountAlias&gt;1000&lt;/accountAlias&gt;

      &lt;name&gt;QA1RSDASER101&lt;/name&gt;

      &lt;startDate&gt;2012-11-15&lt;/startDate&gt;

      &lt;endDate&gt;2012-11-15&lt;/endDate&gt;

  &lt;/GetServerHourlyCharges&gt;

&lt;/soap12:Body&gt;

&lt;/soap12:Envelope&gt;    

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
<h4>JSON (REST)</h4>
<pre>{

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

</pre>

<h4>XML (REST)</h4>
<pre>&lt;ServerHourlyChargesResponse 

  Success="true" 

  Message="OK" 

  StatusCode="0" 

  AccountAlias="RSDA" 

  ServerName="QA1RSDASER101" 

  StartDate="2012-11-14T00:00:00" 

  EndDate="2012-11-15T00:00:00"&gt;

  &lt;Summary MonthlyEstimate="0.0" MonthToDate="0.0" CurrentHour="0.0" PreviousHour="0.0" /&gt;

  &lt;HourlyCharge&gt;

      &lt;ServerHourlyCost Hour="2012-11-14T12:00:00" ProcessorCost="0" MemoryCost="0" StorageCost="0" OSCost="0" /&gt;

      &lt;ServerHourlyCost Hour="2012-11-14T01:00:00" ProcessorCost="0" MemoryCost="0" StorageCost="0" OSCost="0" /&gt;

  &lt;/HourlyCharge&gt;

&lt;/ServerHourlyChargesResponse&gt;

</pre>

<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" 

  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

  xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

  &lt;soap:Body&gt;

      &lt;GetServerHourlyChargesResponse xmlns="http://www.tier3.com/"&gt;

          &lt;GetServerHourlyChargesResult Success="true" 

              Message="OK" 

              StatusCode="0" 

              AccountAlias="RSDA" 

              ServerName="QA1RSDASER101" 

              StartDate="2012-11-14T00:00:00" 

              EndDate="2012-11-15T00:00:00"&gt;

              &lt;Summary MonthlyEstimate="0.0" MonthToDate="0.0" CurrentHour="0.0" PreviousHour="0.0" /&gt;

              &lt;HourlyCharges&gt;

                  &lt;ServerHourlyCost Hour="2012-11-14T12:00:00" ProcessorCost="0" MemoryCost="0" StorageCost="0" OSCost="0" /&gt;

                  &lt;ServerHourlyCost Hour="2012-11-14T01:00:00" ProcessorCost="0" MemoryCost="0" StorageCost="0" OSCost="0" /&gt;

              &lt;/HourlyCharges&gt;

          &lt;/GetServerHourlyChargesResult&gt;

      &lt;/GetServerHourlyChargesResponse&gt;

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
