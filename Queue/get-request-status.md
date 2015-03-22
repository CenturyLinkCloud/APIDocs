{{{
  "title": "GetRequestStatus",
  "date": "11-24-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method can be used to check the status of any of the long running requests which must be performed asynchronously.

## URL

    REST: https://api.ctl.io/REST/Queue/GetRequestStatus/<format> (format = XML | JSON)

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| RequestID | Int | This is the Request ID returned by any of the operations which Queues an async request to perform any given task. | Yes |

### Examples

#### XML

    <QueueStatusRequest>
        <RequestID>50</RequestID>
    </QueueStatusRequest>

#### JSON

    {"RequestID":"50"}

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| RequestDetails | Complex | An entity containing the details of the request. |
| RequestID | Int | The ID of the Request whose details were returned. |
| CurrentStatus | String | The current status of the request, valid values are: `Not Started`, `Executing`, `Succeeded`, `Failed`, and `Resumed`. |
| PercentComplete | Int | The percentage of the work that has been completed on the request. |
| ProgressDesc | String | A description of the progress of the request, for example a description of the step currently being executed. |
| RequestTitle | String | A description of what the Request was created to do. |
| StepNumber | Int | The number of the current step being executed. |
| StatusDate | DateTime | The timestamp (GMT) that the most recent status was recorded on the Request. |

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
      "Success":true,
      "Message":"Request Status successfully retrieved.",
      "StatusCode":0
    }

## Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Create Server request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
