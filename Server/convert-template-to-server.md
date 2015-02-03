{{{
  "title": "ConvertTemplateToServer",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Converts the Template to a Server.

## URL

    REST: https://api.tier3.com/REST/Server/ConvertTemplateToServer/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Server.asmx?op=ConvertTemplateToServer

## Request
### Attributes
<table>
  <tbody>
    <tr>
      <td><strong>Name</strong>
      </td>
      <td><strong>Type</strong>
      </td>
      <td><strong>Description</strong>
      </td>
      <td><strong>Required</strong>
      </td>
    </tr>
    <tr>
      <td>AccountAlias</td>
      <td>String</td>
      <td>The alias of the account that owns the server. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access servers in your sub accounts.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Template. &nbsp;</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Password</td>
      <td>String</td>
      <td>The new administrator/root password for the converted server.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>HardwareGroupID</td>
      <td>Int</td>
      <td>The ID of the hardware group to add the converted server to.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Network</td>
      <td>String</td>
      <td>The name of the network to add the converted server to.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

<h4>JSON</h4>
<pre>{

  "AccountAlias": "UNK",

  "Name": "WA1T3NWEB01",

  "Password": "password",

  "HadwareGroupID": 1,

  "Network": "VLAN113_172.21.113"

}</pre>

<h4>XML</h4>
<pre>&lt;ConvertTemplateToServerRequest&gt;

    &lt;AccountAlias&gt;ACCT&lt;/AccountAlias&gt;

    &lt;Name&gt;WEB&lt;/Name&gt;

    &lt;Password&gt;password&lt;/Password&gt;

    &lt;HardwareGroupID&gt;1&lt;/HardwareGroupID&gt;

    &lt;Network&gt;VLAN113_172.21.113&lt;/Network&gt;

&lt;/ConvertTemplateToServerRequest&gt;</pre>

## Response
### Attributes
<table>
  <tbody>
    <tr>
      <td><strong>Name</strong>
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
      <td>RequestID</td>
      <td>Int</td>
      <td>The ID of the Queued request.Status of the request can be obtained by calling the&nbsp;<a href="http://help.tier3.com/entries/20561586-get-deployment-status">GetDeploymentStatus</a>&nbsp;method.</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{<br />    "RequestID":1,<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0<br />}</pre>

<h4>XML</h4>
<pre>&lt;QueuedItemResponse Success="true" Message="Success" StatusCode="0"&gt;<br />&nbsp; &nbsp; &lt;RequestID&gt;1&lt;/RequestID&gt;<br />&lt;/QueuedItemResponse&gt;</pre>

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
      <td>
        <p>Resource Not Found. &nbsp;</p>
        <p>A Server with the specified Name cannot be found&nbsp;
          <br />- OR -
          <br />A Hardware Group with the specified ID cannot be found&nbsp;</p>
      </td>
    </tr>
    <tr>
      <td>6</td>
      <td>
        <p>Invalid Operation. &nbsp;Template must be in an active state.</p>
      </td>
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
      <td>Password Required.</td>
    </tr>
    <tr>
      <td>1510</td>
      <td>Network Required.</td>
    </tr>
  </tbody>
</table>