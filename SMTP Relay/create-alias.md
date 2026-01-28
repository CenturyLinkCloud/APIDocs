{{{
  "title": "CreateAlias",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method will create a new SMTP Relay alias.

## URL

    REST: https://api.ctl.io/REST/SMTPRelay/CreateAlias/<format> (format = XML | JSON)

## Request

### Attributes

None.

### Examples

#### JSON

N/A

#### XML

N/A

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| RelayAlias | String | The new Relay Alias created for your account. |
| Password | String | The password associated with the new Relay Alias. |

### Examples

#### XML

    <CreateAliasResponse Success="true" Message="Alias has been created." StatusCode="0" RelayAlias="ZZZ1-relay@t3mx.com" Password="password" />

#### JSON

    {
      "Success":true,
      "Message":"Alias has been disabled.",
      "StatusCode":0,
      "RelayAlias":"ZZZ1-relay@t3mx.com",
      "Password":"password"
    }

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | CreateAlias request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
| 400 | You have reached the SMTP Relay Alias limit set on your account. Contact the support to increase your account limit if you need more. |
