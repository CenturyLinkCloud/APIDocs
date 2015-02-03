{{{
  "title": "GetAccounts",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets details of the API user's account and any sub-accounts. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Account/GetAccounts/&lt;format&gt; (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Account.asmx?op=AccountsResponseMsg

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
      <td>None</td>
    </tr>
  </tbody>
</table>

### Examples

#### XML (SOAP)
<pre>&lt;soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

      xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

      xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"&gt;

&lt;soap:Body&gt;

  &lt;AccountsResponseMsg xmlns="http://www.tier3.com/" /&gt;

&lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;  

</pre> 

### Response
## Attributes
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
      <td>Account[]</td>
      <td>Complex</td>
      <td>The list of accounts (see below)</td>
    </tr>
  </tbody>
</table>

### Account Attributes
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
      <td>Short name associated with the parent account.</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>Data center alias (3 letters). List of data center alias is retrieved from <a>GetLocations</a> operation.</td>
    </tr>
    <tr>
      <td>BusinessName</td>
      <td>String</td>
      <td>Full business name associated with the account.</td>
    </tr>
    <tr>
      <td>IsActive</td>
      <td>Boolean</td>
      <td>True/False indicator of whether the account is active or not.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON (REST)
<pre>{<br />     "Accounts":[<br />       {"AccountAlias":"1001","ParentAlias":"1000","Location":"WA1","BusinessName":"Example Business Name","IsActive":true},<br />       {"AccountAlias":"1002","ParentAlias":"1001","Location":"WA1","BusinessName":"Example Department","IsActive":true}<br />     ],<br />     "Success":true,<br />     "Message":"Accounts successfully queried.",<br />     "StatusCode":0<br />}</pre>

#### XML (REST)
<pre>&lt;AccountsResponse Success="true" Message="Accounts successfully queried." StatusCode="0"&gt;<br />     &lt;Accounts&gt;<br />       &lt;Account AccountAlias="1001" ParentAlias="1000" Location="WA1" BusinessName="Example Business Name" IsActive="true"/&gt;<br />       &lt;Account AccountAlias="1002" ParentAlias="1001" Location="WA1" BusinessName="Example Department" IsActive="true" /&gt;<br />     &lt;/Accounts&gt;<br />&lt;/AccountsResponse&gt;</pre>

#### XML (SOAP)
<pre>&lt;soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"&gt;

&lt;soap:Body&gt;

  &lt;AccountsResponseMsgResponse xmlns="http://www.tier3.com/"&gt;

    &lt;AccountsResponseMsgResult&gt;

      &lt;Accounts&gt;

        &lt;Account AccountAlias="1001" ParentAlias="1000" Location="WA1" BusinessName="Example Business Name" IsActive="true" /&gt;

        &lt;Account AccountAlias="1002" ParentAlias="1001" Location="WA1" BusinessName="Example Department" IsActive="true" /&gt;

      &lt;/Accounts&gt;

    &lt;/AccountsResponseMsgResult&gt;

  &lt;/AccountsResponseMsgResponse&gt;

&lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;

</pre>

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
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>
