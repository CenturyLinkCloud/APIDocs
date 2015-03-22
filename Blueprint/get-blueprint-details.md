{{{
  "title": "Get Blueprint Details",
  "date": "10-30-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the full details of the specified Blueprint.

## URL

    REST: https://api.ctl.io/REST/Blueprint/GetBlueprintDetails/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Blueprints.asmx?op=GetBlueprintDetailsResponseMsg

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| ID | Int | The ID of the Blueprint to retrieve details for. | Yes |

### Examples

#### JSON

    { "ID": "1" }

#### XML

    <BlueprintRequest>
        <ID>1</ID>
    </BlueprintRequest>


## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| BlueprintDetails | Complex (see below) | The Blueprint details (see below) |

### BlueprintDetails Attributes

| Name | Type | Description |
| --- | --- | --- |
| Author | String | The name of the company that authored the Blueprint. |
| Capabilities | String[] | List of capabilities that the Blueprint has been tagged with. |
| Description | String | A long description of the Blueprint. |
| ID | Int | The ID of the Blueprint |
| Name | String | The name of the Blueprint. |
| Status | Int | The status of the Blueprint.<br/>1 = Active<br/>3 = Deleted<br/>4 = Under Construction |
| Visibility | Int | The visibility of the Blueprint.<br/>1 = Public<br/>2 = Private |

### Examples

#### JSON

    {
      "BlueprintDetails":{
        "ID":1,
        "Name":"Blueprint 01",
        "Visibility":1,
        "Status":1
        "Author":"",
        "Capabilities":["Web Applications","CDN"],
        "Description":"This is the first Blueprint"
      },
      "Success":true,
      "Message":"Success",
      "StatusCode":0
    }

#### XML

    <GetBlueprintDetailsResponse Success="true" Message="Success" StatusCode="0">
        <BlueprintDetails ID="1" Status="1" Visibility="1">
            <Name>Blueprint 01</Name>
            <Author></Author>
            <Description>This is the first Blueprint</Description>
        </BlueprintDetails>
    </GetBlueprintDetailsResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A Blueprint with the specified ID cannot be found. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
