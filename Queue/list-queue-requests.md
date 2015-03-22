{{{
  "title": "ListQueueRequests",
  "date": "10-13-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method can be used to get a list of Queued requests and their current status details.

## URL

    REST: https://api.ctl.io/REST/Queue/ListQueueRequests/<format> (format = XML | JSON)

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| ItemStatusType | Int | This value indicates the types of statuses you want to get. Valid values are: <br/>1- All<br/>2 - Pending<br/>3 - Complete<br/>4 - Error | Yes |

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

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Requests | List | A List of QueueItem entities. |
| QueueItem | Complex | An entity containing the details of the request. |
| RequestID | Int | The ID of the Request whose details were returned. |
| CurrentStatus | String | The current status of the request, valid values are: `Not Started`, `Executing`, `Succeeded`, `Failed`, and `Resumed`. |
| PercentComplete | Int | The percentage of the work that has been completed on the request. |
| ProgressDesc | String | A description of the progress of the request, for example a description of the step currently being executed. |
| RequestTitle | String | A description of what the Request was created to do. |
| StepNumber | Int | The number of the current step being executed. |
| StatusDate | DateTime | The timestamp (GMT) that the most recent status was recorded on the Request. |

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
      "Requests": [
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

| Status Code | Description |
| --- | --- |
| 0 | Create Server request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 901 | The ItemStatus value is invalid. |
