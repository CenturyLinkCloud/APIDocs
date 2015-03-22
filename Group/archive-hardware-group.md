{{{
  "title": "ArchiveHardwareGroup",
  "date": "10-29-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Archives all Servers in the Group and then archives the Group.

## URL

    REST: https://api.ctl.io/REST/Group/ArchiveHardwareGroup/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Group.asmx?op=ArchiveHardwareGroup

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the group. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access groups in your sub accounts. | No |
| ID | Int | The ID of the Hardware Group to archive. | Yes |

#### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "ID": 1
    }

#### XML

    <GroupRequest>
        <AccountAlias>ACCT</AccountAlias>
        <ID>1</ID>
    </GroupRequest>

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
| 5 | Resource Not Found.  A Group with the specified ID cannot be found. |
| 6 | Invalid Operation.  Group must be in an active state. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
