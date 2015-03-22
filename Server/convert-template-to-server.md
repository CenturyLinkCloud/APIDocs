{{{
  "title": "ConvertTemplateToServer",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Converts the Template to a Server.

## URL

    REST: https://api.ctl.io/REST/Server/ConvertTemplateToServer/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=ConvertTemplateToServer

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the server. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access servers in your sub accounts. | No |
| Name | String | The name of the Template.   | Yes |
| Password | String | The new administrator/root password for the converted server. | Yes |
| HardwareGroupID | Int | The ID of the hardware group to add the converted server to. | Yes |
| Network | String | The name of the network to add the converted server to. | Yes |

### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "Name": "WA1T3NWEB01",
      "Password": "password",
      "HardwareGroupID": 1,
      "Network": "VLAN113_172.21.113"

    }

#### XML

    <ConvertTemplateToServerRequest>
        <AccountAlias>ACCT</AccountAlias>
        <Name>WEB</Name>
        <Password>password</Password>
        <HardwareGroupID>1</HardwareGroupID>
        <Network>VLAN113_172.21.113</Network>
    </ConvertTemplateToServerRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| RequestID | Int | The ID of the Queued request.Status of the request can be obtained by calling the [Get Deployment Status](../Blueprint/get-deployment-status.md) method. |

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
| 5 | Resource Not Found. A Server with the specified Name cannot be found - OR - A Hardware Group with the specified ID cannot be found |
| 6 | Invalid Operation.  Template must be in an active state. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 1410 | Name Required. |
| 1411 | Password Required. |
| 1510 | Network Required. |
