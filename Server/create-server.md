{{{
  "title": "Create Server",
  "date": "10-23-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Creates a new Server.

## URL

    REST: https://api.tier3.com/REST/Server/CreateServer/&lt;format&gt;
    SOAP: https://api.tier3.com/SOAP/Server.asmx?op=CreateServer

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
      <td>The alias of the account to own the server. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to create servers in your sub accounts.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>LocationAlias</td>
      <td>String</td>
      <td>The alias of the data center in which to create the server. If not provided, will default to the API user's default data center.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Template</td>
      <td>String</td>
      <td>The name of the template to create the server from</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Alias</td>
      <td>String</td>
      <td>The alias for the server. &nbsp;Limit 6 charcters</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>An optional description for the server. &nbsp;If none is supplied the server name will be used.&nbsp;</td>
      <td>No</td>
    </tr>
    <tr>
      <td>HardwareGroupID</td>
      <td>Int</td>
      <td>The ID of the Hardware Group to add this server to.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ServerType</td>
      <td>Int</td>
      <td>The type of server to create1 = Standard
        <br />2 = Enterprise</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ServiceLevel</td>
      <td>Int</td>
      <td>The service level/performance for the underlying data store1 = Premium
        <br />2 = Standard&nbsp;</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Cpu</td>
      <td>Int</td>
      <td>The number of processors to configure the server with.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>MemoryGB</td>
      <td>Int</td>
      <td>The number of GB of memory to configure the server with.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>ExtraDriveGB</td>
      <td>Int</td>
      <td>Required. Represents the size in GB of an additional drive to add to the server. If no additional drive is needed, pass in a 0 value.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>PrimaryDns</td>
      <td>IPAddress</td>
      <td>The primary DNS to set on the server.If not supplied the default value set on the account will be used.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>SecondaryDns</td>
      <td>IPAddress</td>
      <td>The secondary DNS to set on the server.If not supplied the default value set on the account will be used.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Network</td>
      <td>String</td>
      <td>The name of the network to which to deploy the server.&nbsp; If your account has not yet been assigned a network, leave this blank and&nbsp;one will be assigned automatically.&nbsp; If one or more networks are available, the network name is required.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Password</td>
      <td>String</td>
      <td>The desired Admin/Root password.&nbsp; Please note the password must meet the password strength policy.&nbsp; Leave blank to have the system generate a password.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>CustomFields</td>
      <td>Complex (see below)</td>
      <td>A list of Custom Fields associated to this server (see below)</td>
      <td>No</td>
    </tr>
  </tbody>
</table>

### CustomField Attributes
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
      <td>CustomFieldID</td>
      <td>Int</td>
      <td>Identifier that is associated with the Account Custom Field (Call Account/GetCustomFields for a list of all custom fields set at the account level)</td>
    </tr>
    <tr>
      <td>Value</td>
      <td>String</td>
      <td>For Text: Any value;&nbsp;For Option values, call Account/GetCustomFields to see possible values to pass in. Checkbox values should be "true" or "false".
        <br />
        <br />
      </td>
    </tr>
  </tbody>
</table>

### Examples
<h4>JSON</h4>
<pre>{

  "AccountAlias": "UNK",

  "LocationAlias": "UN1",

  "Template": "WIN2K8R2",

  "Alias": "WEB",

  "Description": "Web server",

  "HardwareGroupID": 1,

  "ServerType": 1,

  "ServiceLevel": 2,

  "Cpu": 2,

  "MemoryGB": 4,

  "ExtraDriveGB": 50,

  "PrimaryDns": "4.2.2.2",

  "SecondaryDns": "4.2.2.3",

  "Network": "VLAN113_172.21.113",

  "CustomFields":[<br />                { "CustomFieldID": 100,"Value": "A test"},<br />                { "CustomFieldID": 101,"Value": "2"},<br />                { "CustomFieldID": 102,"Value": "true"},]}

}</pre>

<h4>XML</h4>
<pre>&lt;CreateServerRequest&gt;

    &lt;AccountAlias&gt;ACCT&lt;/AccountAlias&gt;

    &lt;LocationAlias&gt;QA1&lt;/LocationAlias&gt;

    &lt;Template&gt;UBUNTU-10-32-TEMPLATE&lt;/Template&gt;

    &lt;MemoryGB&gt;1&lt;/MemoryGB&gt;

    &lt;Cpu&gt;1&lt;/Cpu&gt;

    &lt;HardwareGroupID&gt;1234&lt;/HardwareGroupID&gt;    

    &lt;Alias&gt;WHEE&lt;/Alias&gt;

    &lt;Description&gt;Web server&lt;/Description&gt;            

    &lt;ExtraDriveGB&gt;0&lt;/ExtraDriveGB&gt;

    &lt;PrimaryDns&gt;172.17.1.26&lt;/PrimaryDns&gt;

    &lt;SecondaryDns&gt;172.17.1.27&lt;/SecondaryDns&gt;

    &lt;Network&gt;vlan199_172.21.199&lt;/Network&gt;

    &lt;Password&gt;Pass@word1&lt;/Password&gt;

    &lt;ServerType&gt;1&lt;/ServerType&gt;

    &lt;ServiceLevel&gt;2&lt;/ServiceLevel&gt;

    &lt;CustomFields CustomFieldID="100" Value="Test text" /&gt;

    &lt;CustomFields CustomFieldID="104" Value="2" /&gt;

    &lt;CustomFields CustomFieldID="108" Value="true" /&gt;<br />&lt;/CreateServerRequest&gt;

</pre> 

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
      <td>
        <p>The ID of the Queued request.</p>
        <p>Status of the request can be obtained by calling the&nbsp;<a href="http://help.tier3.com/entries/20561586-get-deployment-status">GetDeploymentStatus</a>&nbsp;method.</p>
      </td>
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
      <td>Resource Not Found. &nbsp;A Hardware Group with the specified ID cannot be found.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>500</td>
      <td>Invalid Memory Value.</td>
    </tr>
    <tr>
      <td>501</td>
      <td>Invalid CPU Value.</td>
    </tr>
    <tr>
      <td>502</td>
      <td>Alias Required.</td>
    </tr>
    <tr>
      <td>503</td>
      <td>Alias Length Exceeded.</td>
    </tr>
    <tr>
      <td>541</td>
      <td>Hardware Group ID Required.&nbsp;</td>
    </tr>
    <tr>
      <td>1510</td>
      <td>Network Required.</td>
    </tr>
    <tr>
      <td>1413</td>
      <td>Extra Drive max storage&nbsp;size exceeded.</td>
    </tr>
    <tr>
      <td>1414</td>
      <td>Password does not meet strength requirements.</td>
    </tr>
  </tbody>
</table>