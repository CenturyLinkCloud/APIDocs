{{{
  "title": "List Domain Names",
  "date": "10-13-2014",
  "author": "jw@tier3.com",
  "attachments": []
}}}

<p><strong><em>This API is no longer supported and will no longer be available beginning November 15th, 2012</em></strong></p>

This method retrieves the list of Domain Names that your account has registered with Tier 3.

## URL

<pre>https://api.tier3.com/REST/Domain/ListDomainNames/&lt;format&gt;</pre>
<p>
  <br />
  <br /><strong>ListDomainNames Request Attributes:</strong>
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
      <td>Search</td>
      <td>String</td>
      <td>No</td>
      <td>This text, if provided, will be used as a search value to filter your Domains. If not provided, all Domain Names will be retrieved.</td>
    </tr>
  </tbody>
</table>
<p>
  <br /><strong>Example Messages:</strong>&nbsp;<strong>XML:</strong>
</p>
<pre>&lt;ListDomainNamesRequest&gt;

  &lt;Search&gt;.com&lt;/Search&gt;

&lt;/ListDomainNamesRequest&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

  "Search":".com"

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
<p>
  <br /><strong>Example Responses:</strong>&nbsp;<strong>XML:</strong>
</p>
<pre>&lt;ListDomainNamesResponse Success="true" Message="The domain names were successfuly listed." StatusCode="0"&gt;

  &lt;Domains&gt;

    &lt;DomainName AutoRenew="true" ExpirationDate="2011-05-24T00:00:00" ID="100001" Name="mycompany.com" /&gt;

    &lt;DomainName AutoRenew="false" ExpirationDate="2011-05-24T00:00:00" ID="100001" Name="myotherdomain.com" /&gt;

  &lt;/Domains&gt;

&lt;/ListDomainNamesResponse&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

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

}</pre>
<p>
  <br />
  <br /><strong>Valid Status Codes returned by the ListDomainNames Method:</strong>
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