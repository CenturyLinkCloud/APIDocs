{{{
  "title": "ListQueueRequests",
  "date": "10-13-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method can be used to get a list of Queued requests and their current status details.

## URL

    REST: https://api.ctl.io/REST/Queue/ListQueueRequests/<format>

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
      <td>ItemStatusType</td>
      <td>Int</td>
      <td>This value indicates the types of statuses you want to get. Valid values are:&nbsp;
        <br />
        <br />1- All
        <br />2 - Pending
        <br />3 - Complete
        <br />4 - Error
      </td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### XML

    <ListQueueItemsRequest>

        <ItemStatusType>1</ItemStatusType>

    </ListQueueItemsRequest>

#### JSON

    {

      "ItemStatusType":"1"

    }

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
      <td>Requests</td>
      <td>List</td>
      <td>A List of QueueItem entities.</td>
    </tr>
    <tr>
      <td>QueueItem</td>
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

    <ListQueueItemsResponse Success="true" Message="3 Queue requests were found for your account" StatusCode="0">

        <Requests>

          <QueueItem RequestID="106" RequestTitle="Installing SQL Server on WA1XXLAB01" ProgressDesc="Request completed" StatusDate="2010-06-15T22:31:33.633" PercentComplete="100" CurrentStatus="Succeeded" StepNumber="0" />

          <QueueItem RequestID="105" RequestTitle="Creating Server WA1XXPREM01" ProgressDesc="Request completed" StatusDate="2010-06-15T16:11:03.083" PercentComplete="100" CurrentStatus="Succeeded" StepNumber="0" />

          <QueueItem RequestID="104" RequestTitle="Creating Lab Server WA1XXLAB01" ProgressDesc="Request completed" StatusDate="2010-06-15T15:59:10.76" PercentComplete="100" CurrentStatus="Succeeded" StepNumber="0" />

        </Requests>

    </ListQueueItemsResponse>

#### JSON

    {

      "Requests":[

        {
          "RequestID":106,

          "RequestTitle":"Installing SQL Server on WA1XXLAB01",

          "ProgressDesc":"Request completed",

          "StatusDate":"\/Date(1276666293633)\/",

          "PercentComplete":100,

          "CurrentStatus":"Succeeded",

          "StepNumber":0

        },

        {
          "RequestID":105,

          "RequestTitle":"Creating Server WA1XXPREM01",

          "ProgressDesc":"Request completed",

          "StatusDate":"\/Date(1276643463083)\/",

          "PercentComplete":100,

          "CurrentStatus":"Succeeded",

          "StepNumber":0

        },

        {

          "RequestID":104,

          "RequestTitle":"Creating Lab Server WA1XXLAB01",

          "ProgressDesc":"Request completed",

          "StatusDate":"\/Date(1276642750760)\/",

          "PercentComplete":100,

          "CurrentStatus":"Succeeded",

          "StepNumber":0

        }

      ],

       "Success":true,

      "Message":"15 Queue requests were found for your account",

      "StatusCode":0
    }

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
    <tr>
      <td>901</td>
      <td>The ItemStatus value is invalid.</td>
    </tr>
  </tbody>
</table>