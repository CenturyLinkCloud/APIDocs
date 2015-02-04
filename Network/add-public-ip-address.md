{{{
  "title": "AddPublicIPAddress",
  "date": "2-6-2014",
  "author": "Peter Kowalczyk",
  "attachments": []
}}}

Maps a public IP Address to a Server.

## URL

REST: https://api.tier3.com/REST/Network/AddPublicIPAddress/<format>
SOAP: https://api.tier3.com/SOAP/Network.asmx?op=AddPublicIPAddress

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
      <td>
        <p>&nbsp;The alias of the account that owns the server. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to manage servers in your sub accounts.</p>
      </td>
      <td>No</td>
    </tr>
    <tr>
      <td>ServerName</td>
      <td>String</td>
      <td>
        <p>The name of the server. &nbsp;</p>
      </td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>IPAddress</td>
      <td>String</td>
      <td>
        <p>An&nbsp;existing internal IP Address on the server to use for the mapping. Leaving this blank will assign a new internal IP Address.</p>
      </td>
      <td>
        <p>No</p>
      </td>
    </tr>
    <tr>
      <td>ServerPassword</td>
      <td>String</td>
      <td>
        <p>The existing password, for authentication. Required only if existing internal&nbsp;IP&nbsp;was&nbsp;not provided and new IP&nbsp;must be assigned.</p>
      </td>
      <td>
        <p>Depends</p>
      </td>
    </tr>
    <tr>
      <td>AllowHTTP</td>
      <td>Boolean</td>
      <td>
        <p>&nbsp;The public IP mapping will allow&nbsp;HTTP requests.</p>
      </td>
      <td>
        <p>&nbsp;No</p>
      </td>
    </tr>
    <tr>
      <td>AllowHTTPonPort8080</td>
      <td>Boolean</td>
      <td>
        <p>&nbsp;The public IP mapping will allow&nbsp;HTTP requests on port 8080.</p>
      </td>
      <td>
        <p>&nbsp;No</p>
      </td>
    </tr>
    <tr>
      <td>AllowHTTPS</td>
      <td>Boolean</td>
      <td>
        <p>&nbsp;The public IP mapping will allow&nbsp;HTTPS requests.</p>
      </td>
      <td>
        <p>&nbsp;No</p>
      </td>
    </tr>
    <tr>
      <td>AllowFTP</td>
      <td>Boolean</td>
      <td>
        <p>&nbsp;The public IP mapping will allow&nbsp;FTP requests.</p>
      </td>
      <td>
        <p>&nbsp;No</p>
      </td>
    </tr>
    <tr>
      <td>AllowFTPS</td>
      <td>Boolean</td>
      <td>
        <p>&nbsp;The public IP mapping will allow&nbsp;FTPS requests.</p>
      </td>
      <td>
        <p>&nbsp;No</p>
      </td>
    </tr>
    <tr>
      <td>AllowSFTP</td>
      <td>Boolean</td>
      <td>
        <p>&nbsp;The public IP mapping will allow&nbsp;SFTP requests.</p>
      </td>
      <td>
        <p>&nbsp;No</p>
      </td>
    </tr>
    <tr>
      <td>AllowSSH</td>
      <td>Boolean</td>
      <td>
        <p>&nbsp;The public IP mapping will allow&nbsp;SSH requests.</p>
      </td>
      <td>
        <p>&nbsp;No</p>
      </td>
    </tr>
    <tr>
      <td>AllowRDP</td>
      <td>Boolean</td>
      <td>
        <p>&nbsp;The public IP mapping will allow&nbsp;RDP requests.</p>
      </td>
      <td>
        <p>&nbsp;No</p>
      </td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "AccountAlias": "SUB1",

      "ServerName": "WA1T3NWEB01",

      "IPAddress": "1.1.1.1",

      "ServerPassword": "password",

      "AllowHTTP": true,

      "AllowHTTPonPort8080": false,

      "AllowHTTPS": false,

      "AllowFTP": false,

      "AllowFTPS": false,

      "AllowSFTP": false,

      "AllowSSH": false,

      "AllowRDP": false

    }

#### XML

    <AddIPAddressRequest>

        <AccountAlias>SUB1</AccountAlias>

        <ServerName>WA1T3NWEB01</ServerName>

        <IPAddress>1.1.1.1</IPAddress>

        <ServerPassword>password</ServerPassword>

        <AllowHTTP>true</AllowHTTP>

        <AllowHTTPonPort8080>false</AllowHTTPonPort8080>

        <AllowHTTPS>false</AllowHTTPS>

        <AllowFTP>false</AllowFTP>

        <AllowFTPS>false</AllowFTPS>

        <AllowSFTP>false</AllowSFTP>

        <AllowSSH>false</AllowSSH>

        <AllowRDP>false</AllowRDP>

    </AddIPAddressRequest>

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
      <td>
        <p>Int</p>
      </td>
      <td>This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state.</td>
    </tr>
    <tr>
      <td>RequestID</td>
      <td>
        <p>Int</p>
      </td>
      <td>The ID of the Blueprint Request submitted to perform this operation.You can check the status of this operation by calling the GetRequestStatus method on the Blueprint API.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

     "Success":true,

     "Message":"Success",

     "StatusCode":0,

     "RequestID":1

    }

#### XML

    <QueuedItemResponse Success="true" Message="Success" StatusCode="0" RequestID="1" />

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
      <td>101</td>
      <td>Access Denied - Your API user account does not have access to the account specified.</td>
    </tr>
    <tr>
      <td>506</td>
      <td>Server Name Required.</td>
    </tr>
    <tr>
      <td>514</td>
      <td>Server Password Required.</td>
    </tr>
    <tr>
      <td>1000</td>
      <td>The&nbsp;IP Address provided is not&nbsp;configured on&nbsp;the Server.</td>
    </tr>
  </tbody>
</table>