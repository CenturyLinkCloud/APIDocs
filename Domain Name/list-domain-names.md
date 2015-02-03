{{{
  "title": "List Domain Names",
  "date": "10-13-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

<p><strong><em>This API is no longer supported and will no longer be available beginning November 15th, 2012</em></strong></p>

This method retrieves the list of Domain Names that your account has registered with Tier 3.

## URL

    REST: https://api.tier3.com/REST/Domain/ListDomainNames<format>

## Request

### Attributes

<table>
  <tbody>
    <tr>
      <thead>
      <tr>
        <td>Name</td>
        <td>Type</td>
        <td>Required</td>
        <td>Description</td>
      </tr>
    </thead>
    <tbody>
    </tr>
    <tr>
      <td>Search</td>
      <td>String</td>
      <td>No</td>
      <td>This text, if provided, will be used as a search value to filter your Domains. If not provided, all Domain Names will be retrieved.</td>
    </tr>
  </tbody>
</table>

### Examples

#### XML

    <ListDomainNamesRequest>

      <Search>.com</Search>

    </ListDomainNamesRequest>

#### JSON:

    {

      "Search":".com"

    }

## Response
### Attributes
<table>
  <thead>
    <tr>
      <td>Name</td>
      <td>Type</td>
      <td>Description</td>
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
      <td>Domains</td>
      <td>List</td>
      <td>A list of DomainName objects.</td>
    </tr>
    <tr>
      <td>DomainName</td>
      <td>Complex</td>
      <td>Details of a given Domain Name registration.</td>
    </tr>
    <tr>
      <td>AutoRenew</td>
      <td>Boolean</td>
      <td>True if the domain is set up for Tier 3 to automatically renew it when it is set to expire.</td>
    </tr>
    <tr>
      <td>ExpirationDate</td>
      <td>DateTime</td>
      <td>The date the domain name registration is set to expire.</td>
    </tr>
    <tr>
      <td>ID</td>
      <td>Int</td>
      <td>The internal Tier3 ID of the domain name.</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The domain name that has been registered.</td>
    </tr>
  </tbody>
</table>

### Examples

#### XML

    <ListDomainNamesResponse Success="true" Message="The domain names were successfuly listed." StatusCode="0">

      <Domains>

        <DomainName AutoRenew="true" ExpirationDate="2011-05-24T00:00:00" ID="100001" Name="mycompany.com" />

        <DomainName AutoRenew="false" ExpirationDate="2011-05-24T00:00:00" ID="100001" Name="myotherdomain.com" />

      </Domains>

    </ListDomainNamesResponse>

#### JSON:

    {

      "Domains":[

        {

          "AutoRenew":true,

          "ExpirationDate":"\/Date(1306220400000)\/",

          "ID":1,

          "Name":"mycompany.com"

        },

        {

          "AutoRenew":false,

          "ExpirationDate":"\/Date(1306220400000)\/",

          "ID":2,

          "Name":"myotherdomain.com"

        }

      ],

      "Success":true,

      "Message":"The domain names were successfuly listed.",

      "StatusCode":0

    }

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
      <td>ListDomainNames request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>