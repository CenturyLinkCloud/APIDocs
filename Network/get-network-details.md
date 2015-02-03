{{{
  "title": "Get Network Details",
  "date": "5-1-2013",
  "author": "Peter Kowalczyk",
  "attachments": []
}}}

GetNetworkDetails
<p>Gets the&nbsp;details for a Network and its&nbsp;IP Addresses.</p>
URL
<pre>REST: https://api.tier3.com/REST/Network/GetNetworkDetails/&lt;format&gt;<br />SOAP: https://api.tier3.com/SOAP/Network.asmx?op=GetNetworkDetailsResponseMsg</pre> Request
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
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The Network name.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{

  "AccountAlias": "UNK",

  "Location": "UN1",

  "Name": "vlan_1114_10.81.14"

}</pre>
<h4>XML</h4>
<pre>&lt;GetNetworkDetailsRequest&gt;

    &lt;AccountAlias&gt;UNK&lt;/AccountAlias&gt;

    &lt;Location&gt;UN1&lt;/Location&gt;

    &lt;Name&gt;vlan250_172.21.250&lt;/Name&gt;

&lt;/GetNetworkDetailsRequest&gt;</pre> Response
<h3>Attributes</h3>
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
      <td>NetworkDetails</td>
      <td>Complex</td>
      <td>The&nbsp;NetworkDetails (see below)</td>
    </tr>
  </tbody>
</table>
<h3>NetworkDetails Attributes</h3>
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
      <td>
        <p>The Network name.</p>
      </td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>The friendly name of the network if one has been configured.</td>
    </tr>
    <tr>
      <td>Gateway</td>
      <td>String</td>
      <td>The default gateway for the network.</td>
    </tr>
    <tr>
      <td>NetworkMask</td>
      <td>String</td>
      <td>
        <p>The network mask.</p>
      </td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>
        <p>The Network's home datacenter alias.</p>
      </td>
    </tr>
    <tr>
      <td>IPAddresses</td>
      <td>String</td>
      <td>A list of IPAddress (see below)</td>
    </tr>
  </tbody>
</table>
<h3>IPAddress Attributes</h3>
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
      <td>Address</td>
      <td>String</td>
      <td>
        <p>The IP Address.</p>
      </td>
    </tr>
    <tr>
      <td>AddressType</td>
      <td>String</td>
      <td>
        <p>The type of the IP Address</p>
        <p>RIP - Real IP (internal IP configured on the VLAN)</p>
        <p>MIP - Mapped IP (external IP configured on the Firewall)</p>
        <p>VIP - Virtual IP (external IP configured on the Load Balancer)</p>
      </td>
    </tr>
    <tr>
      <td>IsClaimed</td>
      <td>Boolean</td>
      <td>
        <p>&nbsp;Indicates if the address is claimed or available.</p>
      </td>
    </tr>
    <tr>
      <td>ServerName</td>
      <td>String</td>
      <td>
        <p>&nbsp;The name of the Server using this IP address, if applicable.</p>
      </td>
    </tr>
  </tbody>
</table>
<h3>Examples</h3>
<h4>JSON</h4>
<pre>{

    "Success":true,

    "Message":"Success",

    "StatusCode":0,

    "NetworkDetails":{

        "Name":"vlan250_172.21.250",

        "Description":"vlan250_172.21.250",

        "Gateway":"172.21.250.1",

        "NetworkMask":"255.255.255.0",

        "Location":"WA1",

        "IPAddresses:[

            {"Address":"172.21.250.2", "AddressType":"RIP", 

            "IsClaimed":false, "ServerName":""},

            {"Address":"172.21.250.3", "AddressType":"RIP", 

            "IsClaimed":true, "ServerName":"DEMOFIRST01"}

        ]}

    }

}</pre>
<h4>XML</h4>
<pre>&lt;NetworkDetailsResponse Success="true" Message="Success" StatusCode="0"&gt;

    &lt;NetworkDetails Name="vlan250_172.21.250" Description="vlan250_172.21.250" 

        Gateway="172.21.250.1" NetworkMask="255.255.255.0" Location="WA1"&gt;

        &lt;IPAddresses&gt;

            &lt;IPAddress Address="172.21.250.2" AddressType="RIP" 

            IsClaimed="false" ServerName="" /&gt;

            &lt;IPAddress Address="172.21.250.3" AddressType="RIP" 

            IsClaimed="true" ServerName="DEMOFIRST01" /&gt;

        &lt;/IPAddresses&gt;

    &lt;/NetworkDetails&gt;

&lt;/NetworkDetailsResponse&gt;</pre>
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
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found.&nbsp;&nbsp;A Network with the specified&nbsp;name cannot be found.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1510</td>
      <td>Name&nbsp;Required.</td>
    </tr>
  </tbody>
</table>