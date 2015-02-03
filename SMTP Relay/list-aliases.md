{{{
  "title": "List Aliases",
  "date": "8-8-2011",
  "author": "jw@tier3.com",
  "attachments": []
}}}

ListAliases
<p>This method will s list of all SMTP Relay aliases for your account.
  <br />
  <br /><strong>URL:</strong>
</p>
<pre>https://api.tier3.com/REST/SMTPRelay/ListAliases/&lt;format&gt;</pre>
<p>
  <br />
  <br /><strong>DeleteSite Request Attributes:</strong>None
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
      <td>SMTPRelayAliases</td>
      <td>List</td>
      <td>A list of RelayAlias objects.</td>
    </tr>
    <tr>
      <td>RelayAlias</td>
      <td>Complex</td>
      <td>The details of a Relay Alias instance.</td>
    </tr>
    <tr>
      <td>Alias</td>
      <td>String</td>
      <td>The new Relay Alias created for your account.</td>
    </tr>
    <tr>
      <td>Password</td>
      <td>String</td>
      <td>The password associated with the new Relay Alias.</td>
    </tr>
    <tr>
      <td>Status</td>
      <td>String</td>
      <td>The current status of the Relay Alias (expected values are 'Active', 'Deleted', and 'Disabled)</td>
    </tr>
  </tbody>
</table>
<p>
  <br /><strong>Example Responses:</strong>&nbsp;<strong>XML:</strong>
</p>
<pre>&lt;ListAliasesResponse Success="true" Message="ListAliases completed successfully" StatusCode="0"&gt;

  &lt;SMTPRelayAliases&gt;

    &lt;RelayAlias Alias="ZZZ1-relay@t3mx.com" Password="password" Status="Active" /&gt;

    &lt;RelayAlias Alias="ZZZ2-relay@t3mx.com" Password="password" Status="Deleted" /&gt;

    &lt;RelayAlias Alias="ZZZ3-relay@t3mx.com" Password="password" Status="Disabled" /&gt;

  &lt;/SMTPRelayAliases&gt;

&lt;/ListAliasesResponse&gt;</pre>
<p>
  <br /><strong>JSON:</strong>
</p>
<pre>{

  "SMTPRelayAliases":[

    {

      "Alias":"ZZZ1-relay@t3mx.com",

      "Password":"password",

      "Status":"Active"

    },

    {

      "Alias":"ZZZ2-relay@t3mx.com",

      "Password":"password",

      "Status":"Deleted"

    },

    {

      "Alias":"ZZZ3-relay@t3mx.com",

      "Password":"password",

      "Status":"Disabled"

    }    

  ],

  "Success":true,

  "Message":"ListAliases completed successfully",

  "StatusCode":0

}</pre>
<p>
  <br />
  <br /><strong>Valid Status Codes returned by the ListAliases Method:</strong>
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
      <td>ListAliases request was successfully processed</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>