{{{
  "title": "GetAccounts",
  "date": "4-9-2015",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets details of the API user's account and any sub-accounts. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/Account/GetAccounts/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Account.asmx?op=AccountsResponseMsg

## Request

### Attributes

None.

### Examples

#### XML (SOAP)

    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:xsd="http://www.w3.org/2001/XMLSchema"
          xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
        <AccountsResponseMsg xmlns="http://www.tier3.com/" />
    </soap:Body>
    </soap:Envelope>  

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Account[] | Complex | The list of accounts (see below). |

### Account Attributes

| Name | Type | Description |
| --- | --- | --- |
| AccountAlias | String | Short name associated with the account. |
| ParentAlias | String | Short name associated with the parent account. |
| Location | String | Data center alias (3 letters). List of data center alias is retrieved from <a>GetLocations</a> operation. |
| BusinessName | String | Full business name associated with the account. |
| IsActive | Boolean | True/False indicator of whether the account is active or not. |
| SupportLevel | String | Indicator of support level for the account.<br/>developer,<br/>legacy,<br/>professional,<br/>enterprise |

### Examples

#### JSON (REST)

    {
      "Accounts":[
        {
          "AccountAlias":"1001",
          "ParentAlias":"1000",
          "Location":"WA1",
          "BusinessName":"Example Business Name",
          "IsActive":true
        },
        {
          "AccountAlias":"1002",
          "ParentAlias":"1001",
          "Location":"WA1",
          "BusinessName":"Example Department",
          "IsActive":true}
      ],
      "Success":true,
      "Message":"Accounts successfully queried.",
      "StatusCode":0
    }

#### XML (REST)

    <AccountsResponse Success="true" Message="Accounts successfully queried." StatusCode="0">
        <Accounts>
            <Account AccountAlias="1001" ParentAlias="1000" Location="WA1" BusinessName="ExampleBusiness Name" IsActive="true"/>
            <Account AccountAlias="1002" ParentAlias="1001" Location="WA1" BusinessName="Example Department" IsActive="true" />
        </Accounts>
    </AccountsResponse>

#### XML (SOAP)

    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
      <soap:Body>
          <AccountsResponseMsgResponse xmlns="http://www.tier3.com/">
              <AccountsResponseMsgResult>
                  <Accounts>
                      <Account AccountAlias="1001" ParentAlias="1000" Location="WA1" BusinessName="Example Business Name" IsActive="true" />
                      <Account AccountAlias="1002" ParentAlias="1001" Location="WA1" BusinessName="Example Department" IsActive="true" />
                  </Accounts>
              </AccountsResponseMsgResult>
          </AccountsResponseMsgResponse>
      </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error. An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed. You must logon to the API prior to calling this method. |
