{{{
  "title": "Configure Server",
  "date": "5-1-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Configures the CPU, Memory, Group and additional storage for a Server.

## URL

    REST: https://api.ctl.io/REST/Server/ConfigureServer/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=ConfigureServer

## Request

### Attributes
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts. | No |
| Name | String | The name of the server. | Yes |
| HardwareGroupID | Int | The ID of the Hardware Group to add this server to. | Yes |
| Cpu | Int | The number of processors to configure the server with.Valid values are 1, 2 and 4 | Yes |
| MemoryGB | Int | The number of GB of memory to configure the server with.Valid values are between 1 and 16. | Yes |
| AdditionalStorageGB | Int | If greater than 0, the size a new disk to add to the server. | No |
| CustomFields | Complex (see below) | A list of Custom Fields associated to this server (see below) | No |

### CustomField Attributes

| Name | Type | Description |
| --- | --- | --- |
| CustomFieldID | Int | Identifier that is associated with the Account Custom Field (Call Account/GetCustomFields for a list of all custom fields set at the account level) |
| Value | String | For Text: Any value; For Option values, call Account/GetCustomFields to see possible values to pass in. Checkbox values should be "true" or "false". |

### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "Name": "WA1T3NWEB01",
      "HardwareGroupID": 1,
      "Cpu": 2,
      "MemoryGB": 4,
      "AdditionalStorageGB": 50,
      "CustomFields":[
        { "CustomFieldID": 100,"Value": "A test"},
        { "CustomFieldID": 101,"Value": "2"},
        { "CustomFieldID": 102,"Value": "true"}
      ]
    }

#### XML

    <ConfigureServerRequest>
        <AccountAlias>UNK</AccountAlias>
        <Name>WEB</Name>
        <HardwareGroupID>1</HardwareGroupID>
        <Cpu>2</Cpu>
        <MemoryGB>4</MemoryGB>
        <AdditionalStorageGB>50</AdditionalStorageGB>
        <CustomFields CustomFieldID="100" Value="Test text" />
        <CustomFields CustomFieldID="104" Value="2" />
        <CustomFields CustomFieldID="108" Value="true" />
    </ConfigureServerRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| RequestID | Int | The ID of the Queued request. Status of the request can be obtained by calling the [Get Deployment Status](../Blueprint/get-deployment-status.md) method. |

### Examples

#### JSON

    {
      "RequestID":1,
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
| 5 | Resource Not Found. A Hardware Group with the specified ID cannot be found. - OR - A Server with the specified Name cannot be found |
| 6 | Invalid Operation.  Server must be in an active state. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 500 | Invalid Memory Value. |
| 501 | Invalid CPU Value. |
| 541 | Hardware Group ID Required.  |
| 1310 | Name Required. |
| 1413 | Additional Storage max size exceeded. |
