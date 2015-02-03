{{{
  "title": "Create Alias",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}

CreateAlias
<p>This method will create a new SMTP Relay alias.
  <br />
  <br /><strong>URL:</strong>
</p>
<pre>https://api.tier3.com/REST/SMTPRelay/CreateAlias/&lt;format&gt;</pre>
<p>
  <br />
  <br /><strong>DeleteSite Request Attributes:</strong>&nbsp;None
  <br />
  <br /><strong>Example Messages:</strong>&nbsp;<strong>XML:</strong>&nbsp;N/A
  <br />
  <br /><strong>JSON:</strong>&nbsp;N/A
  <br />
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
      <td>RelayAlias</td>
      <td>String</td>
      <td>The new Relay Alias created for your account.</td>
    </tr>
    <tr>
      <td>Password</td>
      <td>String</td>
      <td>The password associated with the new Relay Alias.</td>
    </tr>
  </tbody>
</table>
<p>
  <br /><strong>Example Responses:</strong>&nbsp;<strong>XML:</strong>
</p>
<pre>&lt;CreateAliasResponse Success="true" Message="Alias has been created." StatusCode="0" RelayAlias="ZZZ1-relay@t3mx.com" Password="password" /&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

  "Success":true,

  "Message":"Alias has been disabled.",

  "StatusCode":0,

  "RelayAlias":"ZZZ1-relay@t3mx.com",

  "Password":"password"

}</pre>
<p>
  <br />
  <br /><strong>Valid Status Codes returned by the CreateAlias Method:</strong>
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
      <td>CreateAlias request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>400</td>
      <td>You have reached the SMTP Relay Alias limit set on your account. Contact the&nbsp;<a href="mailto:noc@tier3.com">NOC</a>&nbsp;to increase your account limit if you need more.</td>
    </tr>
  </tbody>
</table>