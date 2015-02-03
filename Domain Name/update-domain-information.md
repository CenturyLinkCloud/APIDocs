{{{
  "title": "Update Domain Information",
  "date": "12-24-2012",
  "author": "jw@tier3.com",
  "attachments": []
}}}

<p><strong><em>This API is no longer supported and will no longer be available beginning November 15th, 2012</em></strong></p>

This method provides the ability to update the AutoRenew attribute of your Domain Name registration.

## URL

    REST: https://api.tier3.com/REST/Domain/UpdateDomainInformation/<format>

## Request

### Attributes
<table>
  <tbody>
    <tr>
      <thead>
      <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Description</th>
        <th>Req.</th>
      </tr>
    </thead>
    <tbody>
    </tr>
    <tr>
      <td>AutoRenew</td>
      <td>Boolean</td>
      <td>True if you wish the domain to automatically renew when it is set to expire. The default value is 'false'.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>DomainName</td>
      <td>String</td>
      <td>The Domain Name that you wish to register.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### XML

    <UpdateDomainInformationRequest>

      <AutoRenew>true</AutoRenew>

      <DomainName>mycompany.com</DomainName>

    </UpdateDomainInformationRequest>

#### JSON

    {

      "AutoRenew":true,

      "DomainName":"mycompany.com"

    }

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
  </tbody>
</table>

### Examples

#### XML

    <DomainResponse Success="true" Message="The domain name was successfully updated." StatusCode="0"/>

#### JSON

    {

      "Success":true,

      "Message":"The domain name was successfully updated.",

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
      <td>UpdateDomainInformation request was successfully processed</td>
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
      <td>5</td>
      <td>Resource not Found: The DomainName does not exist for your account.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>800</td>
      <td>Unknown Error returned from the Domain Name registry, try again later.</td>
    </tr>
    <tr>
      <td>801</td>
      <td>The DomainName attribute is required.</td>
    </tr>
  </tbody>
</table>