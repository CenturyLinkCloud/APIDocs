{{{
  "title": "Get Blueprint Parameters",
  "date": "9-15-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets a the full list of parameters that are required to deploy a Blueprint.

## URL

    REST: https://api.ctl.io/REST/Blueprint/GetBlueprintParameters/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Blueprints.asmx?op=GetBlueprintParamatersResponseMsg

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| ID | Int | The ID of the Blueprint to retrieve parameters for. | Yes |

### Examples

#### JSON

    { "ID":1 }

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
| Parameters | List (see below) | A list of the parameters required to deploy the Blueprint (see below) |

### Parameter Attributes

| Name | Type | Description |
| --- | --- | --- |
| Name | String | The name of the Parameter. |
| Options | List | A list of options to choose from if the Parameter is an Option or MultiSelect type. Each option has 2 attributes: `Name` and `Value`. |
| Regex | String | A regular expression defining any additional validation that the Parameter value must pass. This value is supplied by the Blueprint author. |
| Type | JSON: Int<br/>XML: String | The data type of the Parameter<br/>1/Network =  internal name of an existing network<br/>2/Numeric = numeric value<br/>3/Option = constrained to only one of the listed options<br/>4/Password = password value<br/>5/Server = name of an existing server<br/>6/ServerIP = IP address of an existing server<br/>7/String = string value<br/>8/MultiSelect = value constrained to one or more of the listed options |Â

### Examples

#### JSON

    {
      "ID":1,
      "Parameters":[
        {
          "Name":"T3.ScriptTask.Parameter01",
          "Regex":null,
          "Type":7,
          "Options":[]
        },
        {
          "Name":"T3.ScriptTask.Parameter02",
          "Regex":null,
          "Type":3,
          "Options":[
            {"Name":"Option 1","Value":"1"},
            {"Name":"Option 2","Value":"2"}
          ]
        }
      ],
      "Success":true,
      "Message":"Success",
      "StatusCode":0
     }

#### XML

    <GetBlueprintParamatersResponse Success="true" Message="Success" StatusCode="0">
        <ID>46</ID>
        <Parameters>
              <Parameter Name="T3.ScriptTask.Parameter01" Type="String" />
              <Parameter Name="T3.ScriptTask.Parameter02" Type="Option">
                  <Option Name="Option 1" Value="1"/>
                  <Option Name="Option 2" Value="1"/>
              </Parameter>
          </Parameters>
    </GetBlueprintParamatersResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A Blueprint with the specified ID cannot be found. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
