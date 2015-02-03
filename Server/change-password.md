{{{
  "title": "Change Password",
  "date": "5-1-2013",
  "author": "Peter Kowalczyk",
  "attachments": []
}}}

Updates the Admin/Root password&nbsp;for a Server.

### URL

    REST: https://api.tier3.com/REST/Server/ChangePassword/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Server.asmx?op=ChangePassword

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
      <td>The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the server. &nbsp;</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>CurrentPassword</td>
      <td>String</td>
      <td>The existing password,&nbsp;for authentication.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>NewPassword</td>
      <td>String</td>
      <td>The new password to apply.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{

  "AccountAlias": "UNK",

  "Name": "WA1T3NWEB01",

  "CurrentPassword": "password",

  "NewPassword": "newPassword"

}</pre>

<h4>XML</h4>
<pre>&lt;ChangePasswordRequest&gt;

    &lt;AccountAlias&gt;UNK&lt;/AccountAlias&gt;

    &lt;Name&gt;QA1FMACC554L01&lt;/Name&gt;

    &lt;CurrentPassword&gt;password&lt;/CurrentPassword&gt;

    &lt;NewPassword&gt;newPassword&lt;/NewPassword&gt;

&lt;/ChangePasswordRequest&gt;</pre> 

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
<h4>JSON</h4>
<pre>{<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0<br />}</pre>
<h4>XML</h4>
<pre>&lt;APIResponse Success="true" Message="Success" StatusCode="0" /&gt;</pre>

### Status Codes
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
      <td>Request was successfully processed</td>
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
      <td>Resource Not Found.&nbsp;&nbsp;A Server with the specified Name cannot be found.&nbsp;</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Invalid Operation.&nbsp;&nbsp;Server must be in an active state.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1410</td>
      <td>Name Required.</td>
    </tr>
    <tr>
      <td>1411</td>
      <td>Password&nbsp;Required.&nbsp; Both current and new passwords are required.</td>
    </tr>
  </tbody>
</table>