{{{
  "title": "DeleteTemplate",
  "date": "2-6-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Deletes the Template with the specified name.

## URL

    REST: https://api.ctl.io/REST/Server/DeleteTemplate/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=DeleteTemplate

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the template. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to delete templates in your sub accounts. | No |
| Name | String | The name of the Template to delete. | Yes |

### Examples

#### JSON

    {
      "AccountAlias": "ACCT",
      "Name": "TEMPLATENAME01"
    }

#### XML

    <ServerRequest>
        <AccountAlias>UNK</AccountAlias>
        <Name>TEMPLATENAME01</Name>
    </ServerRequest>

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
      "RequestID:1,
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
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A Template with the specified Name cannot be found. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1410 | Name required.  The name parameter must be specified. |
