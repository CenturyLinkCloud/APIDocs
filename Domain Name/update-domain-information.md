{{{
  "title": "Update Domain Information",
  "date": "12-24-2012",
  "author": "jw@tier3.com",
  "attachments": []
}}}

UpdateDomainInformation
<p><strong><em>This API is no longer supported and will no longer be available beginning November 15th, 2012</em></strong>
</p>
<p>This method provides the ability to update the AutoRenew attribute of your Domain Name registration.
  <br />
  <br /><strong>URL:</strong>
</p>
<pre>https://api.tier3.com/REST/Domain/UpdateDomainInformation/&lt;format&gt;</pre>
<p>
  <br />
  <br /><strong>UpdateDomainInformation Request Attributes:</strong>
</p>
<table>
  <tbody>
    <tr>
      <td><strong>Attribute Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Required</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
    <tr>
      <td>AutoRenew</td>
      <td>Boolean</td>
      <td>No</td>
      <td>True if you wish the domain to automatically renew when it is set to expire. The default value is 'false'.</td>
    </tr>
    <tr>
      <td>DomainName</td>
      <td>String</td>
      <td>Yes</td>
      <td>The Domain Name that you wish to register.</td>
    </tr>
  </tbody>
</table>
<p>
  <br /><strong>Example Messages:</strong>&nbsp;<strong>XML:</strong>
</p>
<pre>&lt;UpdateDomainInformationRequest&gt;

  &lt;AutoRenew&gt;true&lt;/AutoRenew&gt;

  &lt;DomainName&gt;mycompany.com&lt;/DomainName&gt;

&lt;/UpdateDomainInformationRequest&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

  "AutoRenew":true,

  "DomainName":"mycompany.com"

}</pre>
<p>
  <br />
  <br /><strong>Response Attributes:</strong>
</p>
<table>
  <tbody>
    <tr>
      <td><strong>Attribute Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
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
<p>
  <br /><strong>Example Responses:</strong>&nbsp;<strong>XML:</strong>
</p>
<pre>&lt;DomainResponse Success="true" Message="The domain name was successfully updated." StatusCode="0"/&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

  "Success":true,

  "Message":"The domain name was successfully updated.",

  "StatusCode":0

}</pre>
<p>
  <br />
  <br /><strong>Valid Status Codes returned by the UpdateDomainInformation Method:</strong>
</p>
<table>
  <tbody>
    <tr>
      <td><strong>Status Code</strong>
      </td>
      <td><strong>Description</strong>
      </td>
    </tr>
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