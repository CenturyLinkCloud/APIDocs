{{{
  "title": "Remove Alias",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}

RemoveAlias
<p>This method will delete an existing SMTP Relay alias.
  <br />
  <br /><strong>URL:</strong>
</p>
<pre>https://api.tier3.com/REST/SMTPRelay/RemoveAlias/&lt;format&gt;</pre>
<p>
  <br />
  <br /><strong>DeleteSite Request Attributes:</strong>
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
      <td>RelayAlias</td>
      <td>String</td>
      <td>Yes</td>
      <td>The the SMTP relay alias to delete.</td>
    </tr>
  </tbody>
</table>
<p>
  <br /><strong>Example Messages:</strong>&nbsp;<strong>XML:</strong>
</p>
<pre>&lt;SMTPUserRequest&gt;

    &lt;RelayAlias&gt;ZZZ1-relay@t3mx.com&lt;/RelayAlias&gt;

&lt;/SMTPUserRequest&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

  "RelayAlias":"ZZZ1-relay@t3mx.com"

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
<pre>&lt;APIResponse Success="true" Message="Alias has been deleted." StatusCode="0" /&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

  "Success":true,

  "Message":"Alias has been deleted.",

  "StatusCode":0 

}</pre>
<p>
  <br />
  <br /><strong>Valid Status Codes returned by the RemoveAlias Method:</strong>
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
      <td>RemoveAlias request was successfully processed</td>
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
      <td>SMTP Relay alias does not exist for your account.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>401</td>
      <td>RelayAlias attribute is required.</td>
    </tr>
    <tr>
      <td>402</td>
      <td>Relay alias has already been deleted.</td>
    </tr>
  </tbody>
</table>