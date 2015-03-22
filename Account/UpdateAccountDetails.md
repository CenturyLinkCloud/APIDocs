{{{
  "title": "UpdateAccountDetails",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Make changes to an existing account in the  system. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/Account/UpdateAccountDetails/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Account.asmx?op=UpdateAccountDetails

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | Four character account alias. | Yes |
| BusinessName | String | Long form business name associated with the account. | Yes |
| Address1 | String | Street address associated with the account. | Yes |
| Address2 | String | Secondary street address associated with the account. | No |
| City | String | City associated with the account. | Yes |
| StateProvince | String | State or province associated with the account. | Yes |
| PostalCode | String | Postal code associated with the account. | Yes |
| Country | String | Country associated with the account. | Yes |
| Telephone | String | Telephone number associated with the account. | Yes |
| Fax | String | Fax number associated with the account. | No |
| TimeZone | String | Timezone of the account holder. Timezone must be one of the values in the list below, otherwise the value is set to the parent account's Timezone. | Yes |
| ShareParentNetworks | Boolean | Determines whether this account shares the networks of the parent account. | Yes |

### Examples

#### JSON (REST)

    {
      "AccountAlias":"1001",
      "BusinessName":"Demo Biz",
      "Address1":"110 110th Avenue",
      "Address2":null,
      "City":"Bellevue",
      "StateProvince":"WA",
      "PostalCode":"98004",
      "Country":"USA",
      "Telephone":"877-388-4373",
      "Fax":null,
      "TimeZone":"Pacific Standard Time",
      "ShareParentNetworks":"true"
    }

#### XML (REST)

    <UpdateAccountDetailsRequest>
        <AccountAlias>1001</AccountAlias>
        <BusinessName>Demo Biz</BusinessName>
        <Address1>110 110th Avenue</Address1>
        <Address2>Suite 520</Address2>
        <City>Bellevue</City>
        <StateProvince>WA</StateProvince>
        <PostalCode>98004</PostalCode>
        <Country>USA</Country>
        <Telephone>877-388-4373</Telephone>
        <Fax></Fax>
        <TimeZone>Pacific Standard Time</TimeZone>
        <ShareParentNetworks>true</ShareParentNetworks>
    </UpdateAccountDetailsRequest>

#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema"
      xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
        <soap12:Body>
            <UpdateAccountDetails xmlns="http://www.tier3.com/">
                <request>
                    <AccountAlias>1001</AccountAlias>
                    <BusinessName>Demo Biz</BusinessName>
                    <Address1>110 110th Avenue</Address1>
                    <Address2>Suite 520</Address2>
                    <City>Bellevue</City>
                    <StateProvince>WA</StateProvince>
                    <PostalCode>98004</PostalCode>
                    <Country>USA</Country>
                    <Telephone>877-388-4373</Telephone>
                    <Fax></Fax>
                    <TimeZone>Pacific Standard Time</TimeZone>
                    <ShareParentNetworks>true</ShareParentNetworks>
                </request>
            </UpdateAccountDetails>
        </soap12:Body>
    </soap12:Envelope>

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
| Status | Int | Indicator of whether the account is active or not.<br/>Active = 1<br/> Inactive = 0 |
| ShareParentNetworks | Boolean | True/false flag indicating whether this account shares the networks of its parent. |

### Examples

#### JSON (REST)

    {
      "AccountDetails":{
        "AccountAlias":"1001",
        "ParentAlias":"1000",
        "Location":"WA1",
        "BusinessName":"Demo Biz"
        "Address1":"110 110th Avenue",
        "Address2":null,
        "City":"Bellevue",
        "StateProvince":"WA",
        "PostalCode":"98004",
        "Country":"USA",
        "Telephone":"877-388-4373",
        "Fax":null,
        "TimeZone":"Pacific Standard Time",
        "Status":1,
        "ShareParentNetworks":true
      },
      "Success":true,
      "Message":"Account details successfully updated.",
      "StatusCode":0
    }

#### XML (REST)

    <AccountDetailsResponse Success="true" Message="Account details successfully updated." StatusCode="0">
         <AccountDetails AccountAlias="1001" ParentAlias="1000" Location="WA1" TimeZone="Pacific Standard Time" Status="1" ShareParentNetworks="true">
             <BusinessName>Demo Biz</BusinessName>
             <Address1>110 110th Avenue</Address1>
             <Address2>Suite 520</Address2>
             <City>Bellevue</City>
             <StateProvince>WA</StateProvince>
             <PostalCode>98004</PostalCode>
             <Country>USA</Country>
             <Telephone>877-388-4373</Telephone>
             <Fax />
         </AccountDetails>
    </AccountDetailsResponse>

#### XML (SOAP)

    <soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:xsd="http://www.w3.org/2001/XMLSchema">
        <soap:Body>
            <UpdateAccountDetailsResponse xmlns="http://www.tier3.com/">
                <UpdateAccountDetailsResult Success="true" Message="Account details successfully updated." StatusCode="0">
                    <AccountDetails AccountAlias="1001" ParentAlias="1000" Location="WA1" TimeZone="Pacific Standard Time" Status="1" ShareParentNetworks="true">
                        <BusinessName>Demo Biz</BusinessName>
                        <Address1>110 110th Avenue</Address1>
                        <Address2>Suite 520</Address2>
                        <City>Bellevue</City>
                        <StateProvince>WA</StateProvince>
                        <PostalCode>98004</PostalCode>
                        <Country>USA</Country>
                        <Telephone>877-388-4373</Telephone>
                        <Fax />
                    </AccountDetails>
                </UpdateAccountDetailsResult>
            </UpdateAccountDetailsResponse>
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
| 1601 | Address Required.  You must provide a primary address when calling this method. |
| 1602 | Business Name Required.  You must provide a business name when calling this method. |
| 1603 | City Required.  You must provide a city name when calling this method. |
| 1604 | Country Required.  You must provide a country name when calling this method. |
| 1605 | Postal Code Required.  You must provide a postal code when calling this method. |
| 1606 | State Province Required.  You must provide a state or province name when calling this method. |
| 1607 | Telephone Required.  You must provide a telephone number when calling this method. |
| 1608 | TimeZone Required.  You must provide a timezone value when calling this method. |
| 1610 | Postal Code Required.  You must provide a primary location when calling this method. |
| 1613 | Email Address Required.  You must provide an email address when calling this method. |
| 1610 | Postal Code Required.  You must provide a primary location when calling this method. |

### Valid Timezone Entries

- Dateline Standard Time
- UTC-11
- Hawaiian Standard Time
- Alaskan Standard Time
- Pacific Standard Time (Mexico)
- Pacific Standard Time
- US Mountain Standard Time
- Mountain Standard Time (Mexico)
- Mountain Standard Time
- Central America Standard Time
- Central Standard Time
- Central Standard Time(Mexico)
- Canada Central Standard Time
- SA Pacific Standard Time
- Eastern Standard Time
- US Eastern Standard Time
- Venezuela Standard Time
- Paraguay Standard Time
- Atlantic Standard Time
- Central Brazilian Standard Time
- SA Western Standard Time
- Pacific SA Standard Time
- Newfoundland Standard Time
- E. South America Standard Time
- Argentina Standard Time
- SA Eastern Standard Time
- Greenland Standard Time
- Montevideo Standard Time
- Bahia Standard Time
- UTC-02
- Mid-Atlantic Standard Time
- Azores Standard Time
- Cape Verde Standard Time
- Morocco Standard Time
- UTC
- GMT Standard Time
- Greenwich Standard Time
- W. Europe Standard Time
- Central Europe Standard Time
- Romance Standard Time
- Central European Standard Time
- W. Central Africa Standard Time
- Namibia Standard Time
- Jordan Standard Time
- GTB Standard Time
- Middle East Standard Time
- Egypt Standard Time
- Syria Standard Time
- South Africa Standard Time
- FLE Standard Time
- Turkey Standard Time
- Israel Standard Time
- E. Europe Standard Time
- Arabic Standard Time
- Kaliningrad Standard Time
- Arab Standard Time
- E. Africa Standard Time
- Iran Standard Time
- Arabian Standard Time
- Azerbaijan Standard Time
- Russian Standard Time
- Mauritius Standard Time
- Georgian Standard Time
- Caucasus Standard Time
- Afghanistan Standard Time
- Pakistan Standard Time
- West Asia Standard Time
- India Standard Time
- Sri Lanka Standard Time
- Nepal Standard Time
- Central Asia Standard Time
- Bangladesh Standard Time
- Ekaterinburg Standard Time
- Myanmar Standard Time
- SE Asia Standard Time
- N. Central Asia Standard Time
- China Standard Time
- North Asia Standard Time
- Singapore Standard Time
- W. Australia Standard Time
- Taipei Standard Time
- Ulaanbaatar Standard Time
- North Asia East Standard Time
- Tokyo Standard Time
- Korea Standard Time
- Cen. Australia Standard Time
- AUS Central Standard Time
- E. Australia Standard Time
- AUS Eastern Standard Time
- West Pacific Standard Time
- Tasmania Standard Time
- Yakutsk Standard Time
- Central Pacific Standard Time
- Vladivostok Standard Time
- New Zealand Standard Time
- UTC+12
- Fiji Standard Time
- Magadan Standard Time
- Kamchatka Standard Time
- Tonga Standard Time
- Samoa Standard Time
