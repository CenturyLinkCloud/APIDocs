{{{
  "title": "GetAccountDetails",
  "date": "03-11-2015",
  "author": "Scott Densmore",
  "attachments": []
}}}

Gets all of the contact information and settings for a given account. Calls to this operation must include an authorization cookie acquired from the <a href="/api-docs#authentication-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Account/GetAccountDetails/<format> (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Account.asmx?op=GetAccountDetails

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
      <td>AccountAlias</td>
      <td>String</td>
      <td>Short code for a particular account.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

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
      <td>Complex</td>
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
        <p>Active&nbsp;=&nbsp;1,
          <br />Disabled&nbsp;=&nbsp;2,
          <br />Deleted&nbsp;=&nbsp;3,
          <br />Demo&nbsp;=&nbsp;4</p>
      </td>
    </tr>
    <tr>
      <td>ShareParentNetworks</td>
      <td>Boolean</td>
      <td>True/false flag indicating whether this account shares the networks of its parent.</td>
    </tr>
    <tr>
      <td>SupportLevel</td>
      <td>String</td>
      <td>Indicator of support level for the account.
        <p>developer,
          <br />legacy,
          <br />professional,
          <br />enterprise</p>
      </td>
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

        "ShareParentNetworks":true,

        "SupportLevel":"developer"

      },

      "Success":true,

      "Message":"Account details successfully queried.",

      "StatusCode":0

    }

#### XML (REST)

    <AccountDetailsResponse Success="true" Message="Account details successfully queried." StatusCode="0">

            <AccountDetails AccountAlias="1001" ParentAlias="1000" Location="WA1" TimeZone="Pacific Standard Time" Status="2" ShareParentNetworks="true" SupportLevel="developer">

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

                    <AccountDetails AccountAlias="1001" ParentAlias="1000" Location="WA1" TimeZone="Pacific Standard Time" Status="2" ShareParentNetworks="true" SupportLevel="developer">

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
  </tbody>
</table>
