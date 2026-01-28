{{{
  "title": "ListAliases",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}


This method will list of all SMTP Relay aliases for your account.

## URL

    https://api.ctl.io/REST/SMTPRelay/ListAliases/<format> (format = XML | JSON)

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
| SMTPRelayAliases | List | A list of RelayAlias objects. |
| RelayAlias | Complex | The details of a Relay Alias instance. |
| Alias | String | The new Relay Alias created for your account. |
| Password | String | The password associated with the new Relay Alias. |
| Status | String | The current status of the Relay Alias (expected values are `Active`, `Deleted`, and `Disabled`) |

### Examples

#### XML

    <ListAliasesResponse Success="true" Message="ListAliases completed successfully" StatusCode="0">
      <SMTPRelayAliases>
        <RelayAlias Alias="ZZZ1-relay@t3mx.com" Password="password" Status="Active" />
        <RelayAlias Alias="ZZZ2-relay@t3mx.com" Password="password" Status="Deleted" />
        <RelayAlias Alias="ZZZ3-relay@t3mx.com" Password="password" Status="Disabled" />
      </SMTPRelayAliases>
    </ListAliasesResponse>

#### JSON

    {
      "SMTPRelayAliases":[
        {
          "Alias":"ZZZ1-relay@t3mx.com",
          "Password":"password",
          "Status":"Active"
        },
        {
          "Alias":"ZZZ2-relay@t3mx.com",
          "Password":"password",
          "Status":"Deleted"
        },
        {
          "Alias":"ZZZ3-relay@t3mx.com",
          "Password":"password",
          "Status":"Disabled"
        }
      ],
      "Success":true,
      "Message":"ListAliases completed successfully",
      "StatusCode":0
    }

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | ListAliases request was successfully processed |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed - You must logon to the API prior to calling this method. |
