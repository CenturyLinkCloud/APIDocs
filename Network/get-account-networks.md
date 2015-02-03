{{{
  "title": "Get Account Networks",
  "date": "2-6-2013",
  "author": "Luke Bakken",
  "attachments": []
}}}

GetAccountNetworks
<p>Gets the list of Networks mapped to an account in any Data Center.</p>
URL
<pre>REST: https://api.tier3.com/REST/Network/GetAccountNetworks/&lt;format&gt;<br />SOAP: https://api.tier3.com/SOAP/Network.asmx?op=GetAccountNetworks</pre> Request
<h3>Attributes</h3>
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
      <td>The alias of the account that owns the network. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to get networks in your sub accounts.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>The Network's home datacenter alias.&nbsp; If blank, the account home datacenter location is assumed.</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{

  "AccountAlias": "UNK",

  "Location": "UN1"

}</pre>
<h4>XML</h4>
<pre>&lt;NetworkRequest&gt;

    &lt;AccountAlias&gt;UNK&lt;/AccountAlias&gt;

    &lt;Location&gt;UN1&lt;/Location&gt;

&lt;/NetworkRequest&gt;</pre> Response
<h3>Attributes</h3>
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
      <td>Networks</td>
      <td>Complex</td>
      <td>
        <p>A list of Network (see below)</p>
      </td>
    </tr>
  </tbody>
</table>
<h3>Network Attributes</h3>
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
      <td>Name</td>
      <td>String</td>
      <td>
        <p>The name of the Network.</p>
        <p>This value should be used on other api methods that require a network reference.</p>
      </td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>The friendly name of the network if one has been configured.</td>
    </tr>
    <tr>
      <td>Gateway</td>
      <td>IPAddress</td>
      <td>The default gateway for the network.</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{

  "Networks": [

    {

      "Name": "vlan_1114_10.81.14",

      "Description": "vlan_1114_10.81.14",

      "Gateway": "10.81.14.1",

      "Location": "UN1",

      "AccountAlias": "UNK"

    },

    {

      "Name": "vlan_1241_10.81.141",

      "Description": "vlan_1241_10.81.141",

      "Gateway": "10.81.141.1",

      "Location": "UN1",

      "AccountAlias": "UNK"

    }

  ],

  "Success": true,

  "Message": "Networks successfully queried.",

  "StatusCode": 0

}</pre>
<h4>XML</h4>
<pre>&lt;GetNetworksResponse Success="true" Message="Networks successfully queried." StatusCode="0"&gt;

&lt;Networks&gt;

    &lt;Network Name="vlan_1114_10.81.14" Description="vlan_1114_10.81.14" Gateway="10.81.14.1" Location="UN1" AccountAlias="UNK"/&gt;

    &lt;Network Name="vlan_1241_10.81.141" Description="vlan_1241_10.81.141" Gateway="10.81.141.1" Location="UN1" AccountAlias="UNK"/&gt;

&lt;/Networks&gt;

&lt;/GetNetworksResponse&gt;</pre>
<h3>Status Codes</h3>
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
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>