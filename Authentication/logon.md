{{{
  "title": "Logon",
  "date": "10-13-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

This method is required to be called prior to calling any other method exposed by the CenturyLink Cloud API. This method validates your credentials and writes the Encrypted cookie required to be present for all subsequent calls into the API.

## URL

    REST: https://api.ctl.io/REST/Auth/Logon/

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| APIKey | String | The API access key provided by CenturyLink Cloud. | Yes |
| Password | String | The API password provided by CenturyLink Cloud. | Yes |

### Examples

#### XML

    <LogonRequest>
      <APIKey>apikey</APIKey>
      <Password>password</Password>
    </LogonRequest>

#### JSON

    {
      "APIKey":"apikey",
      "Password":"password"
    }

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |

### Examples

#### XML

    <LogonResponse Success="true" Message="Login Successful" StatusCode="0" />

#### JSON

    {
      "Success":true,
      "Message":"Login Successful",
      "StatusCode":0
    }

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Logon was successful |
| 2 | Unknown Error - An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 100 | Authentication Failed - The APIKey & Password combination were not valid. Verify that the values provided in your message match the values given to you by CenturyLink Cloud. |
