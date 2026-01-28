{{{
  "title": "SuspendAccount",
  "date": "2-14-2013",
  "author": "Richard Seroter",
  "attachments": []
}}}

Disable an existing account in the  system. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/Account/SuspendAccount/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Account.asmx?op=SuspendAccount

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | Four character account alias. | Yes |

### Examples

#### JSON (REST)

    {

      "AccountAlias": "1000"

    }

#### XML (REST)

    <AccountStatusRequest>
      <AccountAlias>1000</AccountAlias>
    </AccountStatusRequest>

#### XML (SOAP

    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"
            xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
      <soap:Body>
        <SuspendAccount xmlns="http://www.tier3.com/">
          <request>
             <AccountAlias>1000</AccountAlias>
          </request>
        </SuspendAccount>
      </soap:Body>
    </soap:Envelope>  

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| RequestID | Int | The ID of the Queued request.Status aof the request can be obtained by calling the [Get Deployment Status](../Blueprint/get-deployment-status.md) method. |

### Examples

#### JSON (REST)

    {
      "Success": true,
      "Message": "Account Suspended.",
      "StatusCode": 0,
      "RequestID": 100
    }

#### XML (REST)

    <QueuedItemResponse Success="true" Message="Account Suspended." StatusCode="0">
        <RequestID>100</RequestID>
    </QueuedItemResponse>

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
      <soap:Body>
          <SuspendAccountResponse xmlns="http://www.tier3.com/">
              <QueuedItemResponse Success="true" Message="Account Suspended." StatusCode="0">
                  <ResponseID>100</ResponseID>
              </QueuedItemResponse>
          </SuspendAccountResponse>
      </soap:Body>
    </soap:Envelope>


### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 5 | Resource Not Found.  Provided account alias does not exist. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1600 | Account Alias Required.  You must provide an account alias when calling this method. |
