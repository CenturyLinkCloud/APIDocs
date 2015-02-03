{{{
  "title": "PowerOnServer",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Powers on the server (or resumes from a paused state).

## URL

    REST: https://api.tier3.com/REST/Server/PowerOnServer/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Server.asmx?op=PowerOnServer

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
      <td>The alias of the account that owns the server. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access servers in your sub accounts</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Server to power on.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{

  "AccountAlias": "UNK",

  "Name": "SERVER01"

}</pre>

<h4>XML</h4>
<pre>&lt;ServerRequest&gt;

    &lt;AccountAlias&gt;ACCT&lt;/AccountAlias&gt;

    &lt;Name&gt;SERVER01&lt;/Name&gt;

&lt;/ServerRequest&gt;</pre>

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
    <tr>
      <td>RequestID</td>
      <td>Int</td>
      <td>
        <p>The ID of the Queued request.</p>
        <p>Status of the request can be obtained by calling the&nbsp;<a href="http://help.tier3.com/entries/20561586-get-deployment-status">GetDeploymentStatus</a>&nbsp;method.</p>
      </td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{<br />    "RequestID:1,<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0<br />}</pre>

<h4>XML</h4>
<pre>&lt;QueuedItemResponse Success="true" Message="Success" StatusCode="0"&gt;<br />&nbsp; &nbsp; &lt;RequestID&gt;1&lt;/RequestID&gt;<br />&lt;/QueuedItemResponse&gt;</pre>

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
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;A Server with the specified Name cannot be found.</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Invalid Operation. &nbsp;Server must be in an active state.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1410</td>
      <td>Name required. &nbsp;The name parameter must be specified.</td>
    </tr>
  </tbody>
</table>