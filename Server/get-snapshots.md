{{{
  "title": "GetSnapshots",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the list of Snapshots associated with the server.

## URL

    REST: https://api.tier3.com/REST/Server/GetSnapshots/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Server.asmx?op=GetSnapshots

## Request
### Attributes
<table>
    <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Required</th>
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
      <td>The name of the Server to get Snapshots for.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{

  "Name": "DEMOFIRST01",

  "AccountAlias": "UNK"

}</pre>

<h4>XML</h4>
<pre>&lt;ServerRequest&gt;

    &lt;AccountAlias&gt;ACCT&lt;/AccountAlias&gt;

    &lt;Name&gt;SERVER01&lt;/Name&gt;

&lt;/ServerRequest&gt;</pre>

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
      <td>Snapshots</td>
      <td>Complex (see below)</td>
      <td>
        <p>A list of Snapshots (see below)</p>
      </td>
    </tr>
  </tbody>
</table>

### Snapshot Attributes
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
      <td>Name</td>
      <td>String</td>
      <td>The full name of the Snapshot.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>The description of the Snapshot.</td>
    </tr>
    <tr>
      <td>DateCreated</td>
      <td>DateTime</td>
      <td>The time (in UTC) when the Snapshot was created.</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{<br />    "RequestID:1,<br />    "Success":true,<br />    "Message":"Success",<br />    "StatusCode":0,<br />    "Snapshots":[<br />        {"Name":"2012-01-01-12:00:00","Description":"Snapshot (2012-01-01-12:00:00)","DateCreated":"\/Date(1330047404893)\/"}]<br />}</pre>

<h4>XML</h4>
<pre>&lt;GetSnapshotsResponse Success="true" Message="Successfully retrieved snapshots" StatusCode="0"&gt;<br />    &lt;Snapshots&gt;<br />        &lt;Snapshot&gt;<br />            &lt;Name&gt;2012-01-01-12:00:00&lt;/Name&gt;<br />            &lt;Description&gt;Snapshot (2012-01-01-12:00:00)&lt;/Description&gt;<br />            &lt;DateCreated&gt;2012-01-01T12:00:00.000&lt;/DateCreated&gt;<br />        &lt;/Snapshot&gt;<br />    &lt;/Snapshots&gt;<br />&lt;/GetSnapshotsResponse&gt;</pre>

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
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;A server with the specified name could not be found.</td>
    </tr>
    <tr>
      <td>6</td>
      <td>Invalid Operation. &nbsp;Server must be in an active state.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.
        <br />
        <br />
      </td>
    </tr>
    <tr>
      <td>1410</td>
      <td>Name is required.</td>
    </tr>
  </tbody>
</table>