{{{
  "title": "RemoveAlias",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method will delete an existing SMTP Relay alias.

## URL

    REST: https://api.ctl.io/REST/SMTPRelay/RemoveAlias/<format> (format = XML | JSON)

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| RelayAlias | String | The the SMTP relay alias to delete. | Yes |

### Examples

#### JSON

    {
      "RelayAlias":"ZZZ1-relay@t3mx.com"
    }

#### XML

    <SMTPUserRequest>
        <RelayAlias>ZZZ1-relay@t3mx.com</RelayAlias>
    </SMTPUserRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |

### Examples

#### JSON

    {
      "Success":true,
      "Message":"Alias has been deleted.",
      "StatusCode":0
    }

#### XML

    <APIResponse Success="true" Message="Alias has been deleted." StatusCode="0" />

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | RemoveAlias request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | SMTP Relay alias does not exist for your account. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 401 | RelayAlias attribute is required. |
| 402 | Relay alias has already been deleted. |
