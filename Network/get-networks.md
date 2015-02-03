{{{
  "title": "Get Networks",
  "date": "12-3-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

GetNetworks
<p>Gets the list of Networks mapped to the account in its Primary Data Center.&nbsp;</p>
URL
<pre>REST: https://api.tier3.com/REST/Network/GetNetworks/&lt;format&gt;<br />SOAP: https://api.tier3.com/SOAP/Network.asmx?op=GetNetworks</pre> Request
<h3>Attributes</h3>
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
      <td>Short code for a particular account. If not provided, then the API user's account is used.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>The alias of the data center in which to create the server. If not provided, will default to the API user's default data center.</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON (REST)</h4>
<pre>{ <br />    "AccountAlias": "1000",<br />    "Location":"WA1"<br />}</pre>
<h4>XML (REST)</h4>
<pre>&lt;Networks&gt;

    &lt;AccountAlias&gt;1000&lt;/AccountAlias&gt;

    &lt;Location&gt;WA1&lt;/Location&gt;

&lt;/Networks&gt;

    </pre>
<h4>XML (SOAP)</h4>
<pre>&lt;soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

    xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

    xmlns:soap12="http://www.w3.org/2003/05/soap-envelope"&gt;

  &lt;soap12:Body&gt;

    &lt;Networks xmlns="http://www.tier3.com/"&gt;

        &lt;AccountAlias&gt;1000&lt;/AccountAlias&gt;<br />&nbsp; &nbsp; &nbsp; &nbsp; &lt;Location&gt;WA1&lt;/Location&gt;

    &lt;/Networks&gt;

  &lt;/soap12:Body&gt;

&lt;/soap12:Envelope&gt;    

</pre>
<p>&nbsp;</p>
Response
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
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>