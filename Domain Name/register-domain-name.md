{{{
  "title": "Register Domain Name",
  "date": "10-13-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

RegisterDomainName
<p><strong><em>This API is no longer supported and will no longer be available beginning November 15th, 2012</em></strong>
</p>
<p>This method registers a new Domain Name with the Tier3 DNS service.
  <br />
  <br /><strong>URL:</strong>
</p>
<pre>https://api.tier3.com/REST/Domain/RegisterDomainName/&lt;format&gt;</pre>
<p>
  <br />
  <br /><strong>RegisterDomainName Request Attributes:</strong>
</p>
<table>
  <tbody>
    <tr>
      <thead>
      <tr>
        <th>Name</th>
        <th>Type</th>
        <th>Req.</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
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
<pre>&lt;RegisterDomainNameRequest&gt;

  &lt;AutoRenew&gt;true&lt;/AutoRenew&gt;

  &lt;DomainName&gt;mycompany.com&lt;/DomainName&gt;

&lt;/RegisterDomainNameRequest&gt;</pre>
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
<p>
  <br /><strong>Example Responses:</strong>&nbsp;<strong>XML:</strong>
</p>
<pre>&lt;DomainResponse Success="true" Message="The domain name was successfully registered." StatusCode="0"/&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

  "Success":true,

  "Message":"The domain name was successfully registered.",

  "StatusCode":0

}</pre>
<p>
  <br />
  <br /><strong>Valid Status Codes returned by the RegisterDomainName Method:</strong>
</p>
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
      <td>RegisterDomainName request was successfully processed</td>
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
    <tr>
      <td>800</td>
      <td>Unknown Error returned from the Domain Name registry, try again later.</td>
    </tr>
    <tr>
      <td>801</td>
      <td>The DomainName attribute is required.</td>
    </tr>
    <tr>
      <td>804</td>
      <td>The DomainName is unavalable.</td>
    </tr>
  </tbody>
</table>