{{{
  "title": "GetRequestStatus",
  "date": "11-24-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

<p><strong>This API has been deprecated. Please use the following API to make requests:</strong></p>

This method can be used to check the status of any of the long running requests which must be performed asynchronously, including CreateServer, CloneServerToLab, and InstallSQLServer. The main input to this method is the Request ID value returned by the above methods.

## URL

    REST: https://api.tier3.com/REST/Queue/GetRequestStatus/<format>

## Request

### Attributes

<table>
  <tbody>
    <tr>
      <thead>
      <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
        <th>Req.</th>
      </tr>
    </thead>
    <tbody>
    </tr>
    <tr>
      <td>RequestID</td>
      <td>Int</td>
      <td>This is the Request ID returned by any of the operations which Queues an async request to perform any given task.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### XML

    <QueueStatusRequest>

        <RequestID>50</RequestID>

    </QueueStatusRequest>

#### JSON

    {"RequestID":"50"}

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

### Examples

#### XML

    <QueueStatusResponse Success="true" Message="Request Status successfully retrieved." StatusCode="0">  

         <RequestDetails RequestID="50" RequestTitle="Creating Server UT1XXLAB01" ProgressDesc="Request completed" StatusDate="2010-05-28T18:48:49.527" PercentComplete="100" CurrentStatus="Succeeded" StepNumber="0" />

    </QueueStatusResponse>

#### JSON

    {

      "RequestDetails": {

        "RequestID":50,

        "RequestTitle":"Creating Server UT1XXLAB01",

        "ProgressDesc":"Request completed",

        "StatusDate":"\/Date(1275097729527)\/",

        "PercentComplete":100,

        "CurrentStatus":"Succeeded",

        "StepNumber":0

      },

      Success":true,

      "Message":"Request Status successfully retrieved.",

      "StatusCode":0

    }

## Status Codes
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