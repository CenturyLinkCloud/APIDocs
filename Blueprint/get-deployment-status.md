{{{
  "title": "Get Deployment Status",
  "date": "7-14-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the status of the specified Blueprint deployment.

## URL

    REST: https://api.ctl.io/REST/Blueprint/GetBlueprintStatus/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Blueprints.asmx?op=GetDeploymentStatusMsg

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| RequestID | Int | The ID of the Blueprint Deployment to retrieve status for. | Yes |
| LocationAlias | String | The location of the Blueprint Deployment to retrieve status for.  If not provided, will default to the API user's default data center. No |
| AccountAlias | String | ID of the account | Yes |

### Examples

#### JSON

    {
      "RequestID": "1",
      "LocationAlias": "WA1"
    }

#### XML

    <GetDeploymentStatusRequest>
        <RequestID>1</RequestID>
        <LocationAlias>WA1</LocationAlias>
    </GetDeploymentStatusRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| RequestID | Int | The ID of the Blueprint deployment request. (Obtained from [DeployBlueprint](deploy-blueprint.md).) |
| CurrentStatus | String | The status of the Blueprint deployment.  Valid values are: `NotStarted`, `Executing`, `Succeeded`, `Failed`, and `Resumed`. |
| Description | String | A detailed description of the current status. |
| PercentComplete | Int | The percentage of the work that has been completed on the request. |
| StatusDate | DateTime | The timestamp (UTC) that the most recent status was recorded on the Request. |
| Step | String | The current step being executed. |
| Servers | Array | An array of strings with the names of any servers built as part of the Blueprint.<br/>This element is only populated when the Request was originally for server creation. |

### Examples

#### JSON

    {
      "RequestID":210,
      "CurrentStatus":"Failed",
      "Description":"Error Building Blueprint",
      "StatusDate":"\/Date(1318480463790)\/",
      "Step":"0",
      "PercentComplete":0,
      "Success":true,
      "Message":"Success",
      "StatusCode":0,
      "Servers":["WA1T3NWEB01"]
    }


#### XML

    <GetDeploymentStatusResponse
      Success="true"
      Message="Success"
      StatusCode="0"
      RequestID="210"
      CurrentStatus="Failed"
      Description="Error Building Blueprint"
      StatusDate="2011-10-12T21:34:23.79"
      Step="0"
      PercentComplete="0"
        <Servers>
            <string>WA1T3NWEB01</string>
        </Servers>
    </GetDeploymentStatusResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A Blueprint with the specified ID cannot be found. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
