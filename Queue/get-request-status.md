{{{
  "title": "Get Request Status",
  "date": "11-24-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

<p><strong>This API has been deprecated. Please use the following API to make requests:</strong>
</p>
<h3><a href="https://t3n.zendesk.com/entries/20561586-Get-Deployment-Status">Get Deployment Status</a></h3> GetRequestStatus
<p>This method can be used to check the status of any of the long running requests which must be performed asynchronously, including CreateServer, CloneServerToLab, and InstallSQLServer. The main input to this method is the Request ID value returned by the
  above methods.
  <br />
  <br /><strong>URL:</strong>
</p>
<pre>https://api.tier3.com/REST/Queue/GetRequestStatus/&lt;format&gt;</pre>
<p>
  <br /><strong>QueueStatusRequestRequest Attributes:</strong>
</p>
<table>
  <tbody>
    <tr>
      <td><strong>Attribute Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Required</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
    <tr>
      <td>RequestID</td>
      <td>Int</td>
      <td>Yes</td>
      <td>This is the Request ID returned by any of the operations which Queues an async request to perform any given task.</td>
    </tr>
  </tbody>
</table>
<p>
  <br /><strong>Example Messages:</strong>
  <br />
  <br /><strong>XML:</strong>
</p>
<pre>&lt;QueueStatusRequest&gt;

    &lt;RequestID&gt;50&lt;/RequestID&gt;

&lt;/QueueStatusRequest&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{"RequestID":"50"}</pre>
<p>
  <br />
  <br /><strong>Response Attributes:</strong>
</p>
<table>
  <tbody>
    <tr>
      <td><strong>Attribute Name</strong>
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
      <td>RequestDetails</td>
      <td>Complex</td>
      <td>An entity containing the details of the request.</td>
    </tr>
    <tr>
      <td>RequestID</td>
      <td>Int</td>
      <td>The ID of the Request whose details were returned.</td>
    </tr>
    <tr>
      <td>CurrentStatus</td>
      <td>String</td>
      <td>The current status of the request, valid values should be:&nbsp;
        <br />
        <br />- Not Started&nbsp;
        <br />- Executing&nbsp;
        <br />- Succeeded&nbsp;
        <br />- Failed&nbsp;
        <br />- Resumed</td>
    </tr>
    <tr>
      <td>PercentComplete</td>
      <td>Int</td>
      <td>The percentage of the work that has been completed on the request.</td>
    </tr>
    <tr>
      <td>ProgressDesc</td>
      <td>String</td>
      <td>A description of the progress of the request, for example a description of the step currently being executed.</td>
    </tr>
    <tr>
      <td>RequestTitle</td>
      <td>String</td>
      <td>A description of what the Request was created to do.</td>
    </tr>
    <tr>
      <td>StepNumber</td>
      <td>Int</td>
      <td>The number of the current step being executed.</td>
    </tr>
    <tr>
      <td>StatusDate</td>
      <td>DateTime</td>
      <td>The timestamp (GMT) that the most recent status was recorded on the Request.</td>
    </tr>
  </tbody>
</table>
<p>
  <br /><strong>Example Responses:</strong>
  <br />
  <br /><strong>XML:</strong>
</p>
<pre>&lt;QueueStatusResponse Success="true" Message="Request Status successfully retrieved." StatusCode="0"&gt;  

     &lt;RequestDetails RequestID="50" RequestTitle="Creating Server UT1XXLAB01" ProgressDesc="Request completed" StatusDate="2010-05-28T18:48:49.527" PercentComplete="100" CurrentStatus="Succeeded" StepNumber="0" /&gt;

&lt;/QueueStatusResponse&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{"RequestDetails":{"RequestID":50,"RequestTitle":"Creating Server UT1XXLAB01","ProgressDesc":"Request completed","StatusDate":"\/Date(1275097729527)\/","PercentComplete":100,"CurrentStatus":"Succeeded","StepNumber":0},

"Success":true,"Message":"Request Status successfully retrieved.","StatusCode":0}</pre>
<p>
  <br />
  <br /><strong>Valid Status Codes returned by the CheckServerRequestStatus Method:</strong>
</p>
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
      <td>Create Server request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>