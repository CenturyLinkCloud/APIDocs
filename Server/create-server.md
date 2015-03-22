{{{
  "title": "Create Server",
  "date": "10-23-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Creates a new Server.

## URL

    REST: https://api.ctl.io/REST/Server/CreateServer/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=CreateServer

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account to own the server. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to create servers in your sub accounts. | No |
| LocationAlias | String | The alias of the data center in which to create the server. If not provided, will default to the API user's default data center. | No |
| Template | String | The name of the template to create the server from | Yes |
| Alias | String | The alias for the server.  Limit 6 charcters | Yes |
| Description | String | An optional description for the server.  If none is supplied the server name will be used.  | No |
| HardwareGroupID | Int | The ID of the Hardware Group to add this server to. | Yes |
| ServerType | Int | The type of server to create1 = Standard<br/>2 = Enterprise | Yes |
| ServiceLevel | Int | The service level/performance for the underlying data store1 = Premium<br/>2 = Standard  | Yes |
| Cpu | Int | The number of processors to configure the server with. | Yes |
| MemoryGB | Int | The number of GB of memory to configure the server with. | Yes |
| ExtraDriveGB | Int | Required. Represents the size in GB of an additional drive to add to the server. If no additional drive is needed, pass in a 0 value. | Yes |
| PrimaryDns | IPAddress | The primary DNS to set on the server.If not supplied the default value set on the account will be used. | No |
| SecondaryDns | IPAddress | The secondary DNS to set on the server.If not supplied the default value set on the account will be used. | No |
| Network | String | The name of the network to which to deploy the server.  If your account has not yet been assigned a network, leave this blank and one will be assigned automatically.  If one or more networks are available, the network name is required. | No |
| Password | String | The desired Admin/Root password.  Please note the password must meet the password strength policy.  Leave blank to have the system generate a password. | No |
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
      "LocationAlias": "UN1",
      "Template": "WIN2K8R2",
      "Alias": "WEB",
      "Description": "Web server",
      "HardwareGroupID": 1,
      "ServerType": 1,
      "ServiceLevel": 2,
      "Cpu": 2,
      "MemoryGB": 4,
      "ExtraDriveGB": 50,
      "PrimaryDns": "4.2.2.2",
      "SecondaryDns": "4.2.2.3",
      "Network": "VLAN113_172.21.113",
      "CustomFields": [
        { "CustomFieldID": 100,"Value": "A test"},
        { "CustomFieldID": 101,"Value": "2"},
        { "CustomFieldID": 102,"Value": "true"}
      ]
    }

#### XML

    <CreateServerRequest>
        <AccountAlias>ACCT</AccountAlias>
        <LocationAlias>QA1</LocationAlias>
        <Template>UBUNTU-10-32-TEMPLATE</Template>
        <MemoryGB>1</MemoryGB>
        <Cpu>1</Cpu>
        <HardwareGroupID>1234</HardwareGroupID>
        <Alias>WHEE</Alias>
        <Description>Web server</Description>
        <ExtraDriveGB>0</ExtraDriveGB>
        <PrimaryDns>172.17.1.26</PrimaryDns>
        <SecondaryDns>172.17.1.27</SecondaryDns>
        <Network>vlan199_172.21.199</Network>
        <Password>Pass@word1</Password>
        <ServerType>1</ServerType>
        <ServiceLevel>2</ServiceLevel>
        <CustomFields CustomFieldID="100" Value="Test text" />
        <CustomFields CustomFieldID="104" Value="2" />
        <CustomFields CustomFieldID="108" Value="true" />
    </CreateServerRequest>

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
| 5 | Resource Not Found.  A Hardware Group with the specified ID cannot be found. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 500 | Invalid Memory Value. |
| 501 | Invalid CPU Value. |
| 502 | Alias Required. |
| 503 | Alias Length Exceeded. |
| 541 | Hardware Group ID Required.  |
| 1510 | Network Required. |
| 1413 | Extra Drive max storage size exceeded. |
| 1414 | Password does not meet strength requirements. |
