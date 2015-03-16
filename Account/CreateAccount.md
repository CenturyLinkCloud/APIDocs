{{{
  "title": "CreateAccount",
  "date": "11-11-2014",
  "author": "Richard Seroter",
  "attachments": []
}}}


Create a brand new (sub) account in the  system. Calls to this operation must include an authorization cookie acquired from the <a href="/api-docs#authentication-logon">Logon operation.</a>

## URL

```
REST: https://api.ctl.io/REST/Account/CreateAccount/<format> (format = XML | JSON)
```
```
SOAP: https://api.ctl.io/SOAP/Account.asmx?op=CreateAccount
```


## Request

### Attributes

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Req.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ParentAlias</td>
      <td>String</td>
      <td>Account alias of the parent account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>New, four character account alias. If left empty, one is automatically generated.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>Location alias of the primary data center for this account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>BusinessName</td>
      <td>String</td>
      <td>Long form business name associated with the account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Address1</td>
      <td>String</td>
      <td>Street address associated with the account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Address2</td>
      <td>String</td>
      <td>Secondary street address associated with the account.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>City</td>
      <td>String</td>
      <td>City associated with the account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>StateProvince</td>
      <td>String</td>
      <td>State or province associated with the account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PostalCode</td>
      <td>String</td>
      <td>Postal code associated with the account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Country</td>
      <td>String</td>
      <td>Country associated with the account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Telephone</td>
      <td>String</td>
      <td>Telephone number associated with the account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Fax</td>
      <td>String</td>
      <td>Fax number associated with the account.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>TimeZone</td>
      <td>String</td>
      <td>Timezone of the account holder. Timezone must be one of the values in <a href="#tz">the table below</a>, otherwise the value is set to the parent account's Timezone.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>ShareParentNetworks</td>
      <td>Boolean</td>
      <td>Determines whether this account shares the networks of the parent account.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>BillingResponsibilityID</td>
      <td>Integer</td>
      <td>Determines the recipient of the bill.
        <p>1 = Account Directly
          <br />2 = Parent Account</p>
      </td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON (REST)

    {

      "ParentAlias":"1000",

      "AccountAlias":"1001",

      "Location":"WA1",

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

      "ShareParentNetworks":"true",

      "BillingResponsibilityID":"2"

    }

#### XML (REST)

    <CreateAccountRequest>

        <ParentAlias>1000</ParentAlias>

        <AccountAlias>1001</AccountAlias>

        <Location>QA1</Location>

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

        <BillingResponsibilityID>2</BillingResponsibilityID>

    </CreateAccountRequest>


#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

                    xmlns:xsd="http://www.w3.org/2001/XMLSchema"

                    xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">

        <soap12:Body>

            <CreateAccount xmlns="http://www.tier3.com/">

                <request>

                <ParentAlias>1000</ParentAlias>

                <AccountAlias>1001</AccountAlias>

                <Location>WA</Location>

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

                <BillingResponsibilityID>2</BillingResponsibilityID>

                </request>

            </CreateAccount>

        </soap12:Body>

    </soap12:Envelope>  

## Response

### Attributes

<table>
  <thead>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
    <tr>
      <td>Success</td>
      <td>Boolean</td>
      <td>True if the request was successful, otherwise False.</td>
    </tr>
    <tr>
      <td>Message</td>
      <td>String</td>
      <td>A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result.</td>
    </tr>
    <tr>
      <td>StatusCode</td>
      <td>Int</td>
      <td>This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state.</td>
    </tr>
    <tr>
      <td>AccountDetails</td>
      <td>Complex (see below)</td>
      <td>The account details</td>
    </tr>
  </tbody>
</table>

### AccountDetails Attributes

<table>
  <thead>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short name associated with the account.</td>
    </tr>
    <tr>
      <td>ParentAlias</td>
      <td>String</td>
      <td>Short name associated with parent account of the queried account.</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>Data center location alias associated with this account.</td>
    </tr>
    <tr>
      <td>BusinessName</td>
      <td>String</td>
      <td>Full name of the business that the account is registered under.</td>
    </tr>
    <tr>
      <td>Address1</td>
      <td>String</td>
      <td>Street address of the business associated with this account.</td>
    </tr>
    <tr>
      <td>Address2</td>
      <td>String</td>
      <td>Secondary street address (if any) of the business associated with this account.</td>
    </tr>
    <tr>
      <td>City</td>
      <td>String</td>
      <td>City of the business associated with this account.</td>
    </tr>
    <tr>
      <td>StateProvince</td>
      <td>String</td>
      <td>State or province of the business associated with this account.</td>
    </tr>
    <tr>
      <td>PostalCode</td>
      <td>String</td>
      <td>Postal code of the business associated with this account.</td>
    </tr>
    <tr>
      <td>Country</td>
      <td>String</td>
      <td>Country of the business associated with this account.</td>
    </tr>
    <tr>
      <td>Telephone</td>
      <td>String</td>
      <td>Telephone number of the business associated with this account.</td>
    </tr>
    <tr>
      <td>Fax</td>
      <td>String</td>
      <td>Fax number (if any) of the business associated with this account.</td>
    </tr>
    <tr>
      <td>TimeZone</td>
      <td>String</td>
      <td>Time zone of the business associated with this account.</td>
    </tr>
    <tr>
      <td>Status</td>
      <td>Int</td>
      <td>Indicator of whether the account is active or not.
        <p>Active = 1
          <br /> Inactive = 0</p>
      </td>
    </tr>
    <tr>
      <td>ShareParentNetworks</td>
      <td>Boolean</td>
      <td>True/false flag indicating whether this account shares the networks of its parent.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON (REST)

    {

      "AccountDetails": {

        "AccountAlias":"1001",

        "ParentAlias":"1000",

        "Location":"WA1",

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

        "Status":1,

        "ShareParentNetworks":true

      },  

      "Success":true,

      "Message":"Account successfully created.",

      "StatusCode":0

    }

#### XML (REST)

    <AccountDetailsResponse Success="true" Message="Account successfully created." StatusCode="0">

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

            <CreateAccountResponse xmlns="http://www.tier3.com/">

                <CreateAccountResult Success="true" Message="Account successfully created." StatusCode="0">

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

                </CreateAccountResult>

            </CreateAccountResponse>

        </soap:Body>

    </soap:Envelope>

### Status Codes

<table>
  <thead>
    <tr>
      <th>Status Code</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;Provided account alias does not exist.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1600</td>
      <td>Account Alias Required. &nbsp;You must provide an account alias when calling this method.</td>
    </tr>
    <tr>
      <td>1601</td>
      <td>Address Required. &nbsp;You must provide a primary address when calling this method.</td>
    </tr>
    <tr>
      <td>1602</td>
      <td>Business Name Required. &nbsp;You must provide a business name when calling this method.</td>
    </tr>
    <tr>
      <td>1603</td>
      <td>City Required. &nbsp;You must provide a city name when calling this method.</td>
    </tr>
    <tr>
      <td>1604</td>
      <td>Country Required. &nbsp;You must provide a country name when calling this method.</td>
    </tr>
    <tr>
      <td>1605</td>
      <td>Postal Code Required. &nbsp;You must provide a postal code when calling this method.</td>
    </tr>
    <tr>
      <td>1606</td>
      <td>State Province Required. &nbsp;You must provide a state or province name when calling this method.</td>
    </tr>
    <tr>
      <td>1607</td>
      <td>Telephone Required. &nbsp;You must provide a telephone number when calling this method.</td>
    </tr>
    <tr>
      <td>1608</td>
      <td>TimeZone Required. &nbsp;You must provide a timezone value when calling this method.</td>
    </tr>
    <tr>
      <td>1609</td>
      <td>Parent Alias Required. &nbsp;You must provide a parent alias when calling this method.</td>
    </tr>
    <tr>
      <td>1610</td>
      <td>Postal Code Required. &nbsp;You must provide a primary location when calling this method.</td>
    </tr>
    <tr>
      <td>1611</td>
      <td>Duplicate Account. &nbsp;You must provide a unique alias and business name when calling this method.</td>
    </tr>
    <tr>
      <td>1613</td>
      <td>Email Address Required. &nbsp;You must provide an email address when calling this method.</td>
    </tr>
    <tr>
      <td>1616</td>
      <td>Invalid Billing Responsibility. &nbsp;You must provide valid billing responsibilty when calling this method.</td>
    </tr>
    <tr>
      <td>1610</td>
      <td>Postal Code Required. &nbsp;You must provide a primary location when calling this method.</td>
    </tr>
  </tbody>
</table>
<p>
  <br />
  <a name="tz"></a>
</p>
<h3>Valid Timezone Entries</h3>
<table>
  <tbody>
    <tr>
      <td><strong>Timezone Value</strong>
      </td>
    </tr>
    <tr>
      <td>Dateline Standard Time
        <br /> UTC-11
        <br /> Hawaiian Standard Time
        <br /> Alaskan Standard Time
        <br /> Pacific Standard Time (Mexico)
        <br /> Pacific Standard Time
        <br /> US Mountain Standard Time
        <br /> Mountain Standard Time (Mexico)
        <br /> Mountain Standard Time
        <br /> Central America Standard Time
        <br /> Central Standard Time
        <br /> Central Standard Time(Mexico)
        <br /> Canada Central Standard Time
        <br /> SA Pacific Standard Time
        <br /> Eastern Standard Time
        <br /> US Eastern Standard Time
        <br /> Venezuela Standard Time
        <br /> Paraguay Standard Time
        <br /> Atlantic Standard Time
        <br /> Central Brazilian Standard Time
        <br /> SA Western Standard Time
        <br /> Pacific SA Standard Time
        <br /> Newfoundland Standard Time
        <br /> E. South America Standard Time
        <br /> Argentina Standard Time
        <br /> SA Eastern Standard Time
        <br /> Greenland Standard Time
        <br /> Montevideo Standard Time
        <br /> Bahia Standard Time
        <br /> UTC-02
        <br /> Mid-Atlantic Standard Time
        <br /> Azores Standard Time
        <br /> Cape Verde Standard Time
        <br /> Morocco Standard Time
        <br /> UTC
        <br /> GMT Standard Time
        <br /> Greenwich Standard Time
        <br /> W. Europe Standard Time
        <br /> Central Europe Standard Time
        <br /> Romance Standard Time
        <br /> Central European Standard Time
        <br /> W. Central Africa Standard Time
        <br /> Namibia Standard Time
        <br /> Jordan Standard Time
        <br /> GTB Standard Time
        <br /> Middle East Standard Time
        <br /> Egypt Standard Time
        <br /> Syria Standard Time
        <br /> South Africa Standard Time
        <br /> FLE Standard Time
        <br /> Turkey Standard Time
        <br /> Israel Standard Time
        <br /> E. Europe Standard Time
        <br /> Arabic Standard Time
        <br /> Kaliningrad Standard Time
        <br /> Arab Standard Time
        <br /> E. Africa Standard Time
        <br /> Iran Standard Time
        <br /> Arabian Standard Time
        <br /> Azerbaijan Standard Time
        <br /> Russian Standard Time
        <br /> Mauritius Standard Time
        <br /> Georgian Standard Time
        <br /> Caucasus Standard Time
        <br /> Afghanistan Standard Time
        <br /> Pakistan Standard Time
        <br /> West Asia Standard Time
        <br /> India Standard Time
        <br /> Sri Lanka Standard Time
        <br /> Nepal Standard Time
        <br /> Central Asia Standard Time
        <br /> Bangladesh Standard Time
        <br /> Ekaterinburg Standard Time
        <br /> Myanmar Standard Time
        <br /> SE Asia Standard Time
        <br /> N. Central Asia Standard Time
        <br /> China Standard Time
        <br /> North Asia Standard Time
        <br /> Singapore Standard Time
        <br /> W. Australia Standard Time
        <br /> Taipei Standard Time
        <br /> Ulaanbaatar Standard Time
        <br /> North Asia East Standard Time
        <br /> Tokyo Standard Time
        <br /> Korea Standard Time
        <br /> Cen. Australia Standard Time
        <br /> AUS Central Standard Time
        <br /> E. Australia Standard Time
        <br /> AUS Eastern Standard Time
        <br /> West Pacific Standard Time
        <br /> Tasmania Standard Time
        <br /> Yakutsk Standard Time
        <br /> Central Pacific Standard Time
        <br /> Vladivostok Standard Time
        <br /> New Zealand Standard Time
        <br /> UTC+12
        <br /> Fiji Standard Time
        <br /> Magadan Standard Time
        <br /> Kamchatka Standard Time
        <br /> Tonga Standard Time
        <br /> Samoa Standard Time</td>
    </tr>
  </tbody>
</table>
