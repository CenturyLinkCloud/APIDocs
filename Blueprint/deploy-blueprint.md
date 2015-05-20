{{{
  "title": "Deploy Blueprint",
  "date": "1-31-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Deploys a Blueprint with the given set of parameter values.

## URL

    REST: https://api.ctl.io/REST/Blueprint/DeployBlueprint/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Blueprints.asmx?op=DeployBlueprint

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| ID | Int | The ID of the Blueprint to deploy. | Yes |
| LocationAlias | string | The alias of the Datacenter where you would like to deploy the blueprint to. If not provided, it will default to your primary datacenter. | No |
| Parameters | List (see below) | A list of Parameter values to use during the deployment of the Blueprint. | Yes |
| CustomFields | Complex (see below) | Custom Fields that need to be set on each server created during blueprint deployment | No |

### Parameter Attributes

| Name | Type | Description |
| --- | --- | --- |
| Name | String | The name of the Parameter being set. |
| Value | String | The value for the Parameter. _This value will be validated based on the type and validation rules specified by the Blueprint Parameter definition._ |

### CustomField Attributes

| Name | Type | Description |
| --- | --- | --- |
| ID | String | Unique identifier that is associated with the Account Custom Field. Call [Account/GetCustomFields](../Account/GetCustomFields.md) for a list of all custom fields set at the account level. |
| Value | String | For Text: Any value; For Option values, call [Account/GetCustomFields](../Account/GetCustomFields.md) to see possible values to pass in. Checkbox values should be "true" or "false". |

### Examples

#### JSON
    {
      "ID": "1",
      "LocationAlias": "WA1",
      "Parameters": [
        { "Name":"T3.BuildServerTask.Password", "Value":"password" },
        { "Name":"T3.BuildServerTask.Network","Value":"VLAN_XXX" },
        { "Name":"T3.BuildServerTask.PrimaryDNS","Value":"192.168.64.19" },
        { "Name":"T3.BuildServerTask.SecondaryDNS","Value":"192.168.64.20" }
      ],
      "CustomFields": [
        { "ID": "ea97c6e09f604eb689dcdc080114b04d","Value": "A test"},
        { "ID": "b9f454f2ae664998acc3302b24330c5b","Value": "2"},
        { "ID": "d1f12de4ce4b4685b72ba632db0685c6","Value": "true"}
      ]
    }

#### XML

    <DeployBlueprintRequest>
        <ID>107</ID>
        <LocationAlias>WA1</LocationAlias>
        <Parameters>
            <Parameter Name="T3.BuildServerTask.Password" Value="Pass@word1" />
            <Parameter Name="T3.BuildServerTask.Network" Value="VLAN_XXX" />
            <Parameter Name="T3.BuildServerTask.PrimaryDNS" Value="192.168.64.19" />
            <Parameter Name="T3.BuildServerTask.SecondaryDNS" Value="192.168.64.20" />
        </Parameters>
        <CustomFields ID="ea97c6e09f604eb689dcdc080114b04d" Value="Test text" />
        <CustomFields ID="b9f454f2ae664998acc3302b24330c5b" Value="2" />
        <CustomFields ID="d1f12de4ce4b4685b72ba632db0685c6" Value="true" />
    </DeployBlueprintRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| RequestID | Int | The ID of the Queued request to deploy the Blueprint. Status of the request can be obtained by calling the [GetDeploymentStatus](../Blueprints/get-deployment-status.md) method. |

### Examples

#### JSON

    {
      "RequestID": 1,
      "Success":true,
      "Message":"Success",
      "StatusCode":0
    }

#### XML

    <QueuedItemResponse Success="true" Message="Success" StatusCode="0">
        <RequestID>1</RequestID>
    </QueuedItemResponse>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 1210 | A required Parameter is missing. |
| 1211 | A Parameter value is invalid. Ensure that the supplied value meets the validation rules of the Blueprint Parameter. |
| 1212 | A Parameter type is invalid. Ensure that the supplied value is convertible to the type defined by the Blueprint Parameter. |
