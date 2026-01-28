{{{
  "title": "Configure Server",
  "date": "5-1-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Configures the CPU, Memory, Group and additional storage for a Server.

<div class="alert alert-warning">
<h2>V2 API Available</h2>
There is an equivalent V2 API that should be used instead. Please use the Servers | <a href="../v2/#servers-set-server-cpumemory">Set Server CPU/Memory</a>, Servers | <a href"../v2/#servers-set-server-disks">Set Server Disks</a>, and Servers | <a href"../v2/#servers-set-server-descriptiongroup">Set Server Description/Group</a> APIs.
</div>

## URL

    REST: https://api.ctl.io/REST/Server/ConfigureServer/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=ConfigureServer

## Request

### Attributes
| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts. | No |
| Name | String | The name of the server. | Yes |
| HardwareGroupUUID | String | The unique identifier of the Hardware Group to add this server to. | Yes |
| Cpu | Int | The number of processors to configure the server with.Valid values are 1, 2 and 4 | Yes |
| MemoryGB | Int | The number of GB of memory to configure the server with.Valid values are between 1 and 16. | Yes |
| AdditionalStorageGB | Int | If greater than 0, the size a new disk to add to the server. | No |
| CustomFields | Complex (see below) | A list of Custom Fields associated to this server (see below) | No |

### CustomField Attributes

| Name | Type | Description |
| --- | --- | --- |
| ID | String | Unique identifier that is associated with the Account Custom Field. Call [Account/GetCustomFields](../Account/GetCustomFields.md) for a list of all custom fields set at the account level. |
| Value | String | For Text: Any value; For Option values, call [Account/GetCustomFields](../Account/GetCustomFields.md) to see possible values to pass in. Checkbox values should be "true" or "false". |tring | For Text: Any value; For Option values, call Account/GetCustomFields to see possible values to pass in. Checkbox values should be "true" or "false". |

### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "Name": "WA1T3NWEB01",
      "HardwareGroupUUID": "8a03fbae8ddfe311b05f00505682315a",
      "Cpu": 2,
      "MemoryGB": 4,
      "AdditionalStorageGB": 50,
      "CustomFields": [
        { "ID": "ea97c6e09f604eb689dcdc080114b04d","Value": "A test"},
        { "ID": "b9f454f2ae664998acc3302b24330c5b","Value": "2"},
        { "ID": "d1f12de4ce4b4685b72ba632db0685c6","Value": "true"}
      ]
    }

#### XML

    <ConfigureServerRequest>
        <AccountAlias>UNK</AccountAlias>
        <Name>WEB</Name>
        <HardwareGroupUUID>8a03fbae8ddfe311b05f00505682315a</HardwareGroupUUID>
        <Cpu>2</Cpu>
        <MemoryGB>4</MemoryGB>
        <AdditionalStorageGB>50</AdditionalStorageGB>
        <CustomFields ID="ea97c6e09f604eb689dcdc080114b04d" Value="Test text" />
        <CustomFields ID="b9f454f2ae664998acc3302b24330c5b" Value="2" />
        <CustomFields ID="d1f12de4ce4b4685b72ba632db0685c6" Value="true" />
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
