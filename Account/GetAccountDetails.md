{{{
  "title": "GetAccountDetails",
  "date": "7-9-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets all of the contact information and settings for a given account. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/Account/GetAccountDetails/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Account.asmx?op=GetAccountDetails

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | Short code for a particular account. | Yes |

### Examples

#### JSON (REST)

    {

      "AccountAlias": "1000"

    }

#### XML (REST)

    <GetAccountDetailsRequest>
        <AccountAlias>1000</AccountAlias>
    </GetAccountDetailsRequest>

#### XML (SOAP)

    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"
            xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
      <soap:Body>
        <GetAccountDetails xmlns="http://www.tier3.com/">
          <request>
             <AccountAlias>1000</AccountAlias>
          </request>
        </GetAccountDetails>
      </soap:Body>
    </soap:Envelope>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| AccountDetails | Complex | The account details |

### AccountDetails Attributes

| Name | Type | Description |
| --- | --- | --- |
| AccountAlias | String | Short name associated with the account. |
| ParentAlias | String | Short name associated with parent account of the queried account. |
| Location | String | Data center location alias associated with this account. |
| BusinessName | String | Full name of the business that the account is registered under. |
| Address1 | String | Street address of the business associated with this account. |
| Address2 | String | Secondary street address (if any) of the business associated with this account. |
| City | String | City of the business associated with this account. |
| StateProvince | String | State or province of the business associated with this account. |
| PostalCode | String | Postal code of the business associated with this account. |
| Country | String | Country of the business associated with this account. |
| Telephone | String | Telephone number of the business associated with this account. |
| Fax | String | Fax number (if any) of the business associated with this account. |
| TimeZone | String | Time zone of the business associated with this account. |
| Status | Int | Indicator of whether the account is active or not.<br/>Active = 1,<br/>Disabled = 2,<br/>Deleted = 3,<br/>Demo = 4 |
| ShareParentNetworks | Boolean | True/false flag indicating whether this account shares the networks of its parent. |

### Examples

#### JSON (REST)

    {
      "AccountDetails": {
        "AccountAlias":"1001",
        "ParentAlias":"1000",
        "Location":"WA1",
        "BusinessName":"Example Business Name",
        "Address1":"110 110th Avenue",
        "Address2":null,
        "City":"Bellevue",
        "StateProvince":"WA",
        "PostalCode":"98004",
        "Country":"USA",
        "Telephone":"877-388-4373",
        "Fax":null,
        "TimeZone":"Pacific Standard Time",
        "Status":2,
        "ShareParentNetworks":true
      },
      "Success":true,
      "Message":"Account details successfully queried.",
      "StatusCode":0
    }

#### XML (REST)

    <AccountDetailsResponse Success="true" Message="Account details successfully queried." StatusCode="0">
        <AccountDetails AccountAlias="1001" ParentAlias="1000" Location="WA1" TimeZone="Pacific Standard Time" Status="2" ShareParentNetworks="true">
            <BusinessName>Example Business Name</BusinessName>
            <Address1>110 110th Avenue</Address1>
            <City>Bellevue</City>
            <StateProvince>WA</StateProvince>
            <PostalCode>98004</PostalCode>
            <Country>USA</Country>
            <Telephone>877-388-4373</Telephone>
        </AccountDetails>
    </AccountDetailsResponse>

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:xsd="http://www.w3.org/2001/XMLSchema">
         <soap:Body>
            <GetAccountDetailsResponse xmlns="http://www.tier3.com/">
                <GetAccountDetailsResult Success="true" Message="Account details successfully queried." StatusCode="0">
                    <AccountDetails AccountAlias="1001" ParentAlias="1000" Location="WA1" TimeZone="Pacific Standard Time" Status="2" ShareParentNetworks="true">
                        <BusinessName>Example Business Name</BusinessName>
                        <Address1>110 110th Avenue</Address1>
                        <City>Bellevue</City>
                	      <StateProvince>WA</StateProvince>
                        <PostalCode>98004</PostalCode>
                        <Country>USA</Country>
                        <Telephone>877-388-4373</Telephone>
                    </AccountDetails>
                </GetAccountDetailsResult>
            </GetAccountDetailsResponse>
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
