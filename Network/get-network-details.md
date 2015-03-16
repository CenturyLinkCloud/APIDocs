{{{
  "title": "GetNetworkDetails",
  "date": "5-1-2013",
  "author": "Peter Kowalczyk",
  "attachments": []
}}}

Gets the details for a Network and its IP Addresses.

## URL

    REST: https://api.ctl.io/REST/Network/GetNetworkDetails/<format>
    SOAP: https://api.ctl.io/SOAP/Network.asmx?op=GetNetworkDetailsResponseMsg

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

### Examples

#### JSON

    {

      "AccountAlias": "UNK",

      "Location": "UN1",

      "Name": "vlan_1114_10.81.14"

    }

#### XML

    <GetNetworkDetailsRequest>

        <AccountAlias>UNK</AccountAlias>

        <Location>UN1</Location>

        <Name>vlan250_172.21.250</Name>

    </GetNetworkDetailsRequest>

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
      <td>NetworkDetails</td>
      <td>Complex</td>
      <td>The&nbsp;NetworkDetails (see below)</td>
    </tr>
  </tbody>
</table>

### NetworkDetails Attributes

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

### IPAddress Attributes

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

### Examples

#### JSON

    {

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

    }

#### XML

    <NetworkDetailsResponse Success="true" Message="Success" StatusCode="0">

        <NetworkDetails Name="vlan250_172.21.250" Description="vlan250_172.21.250" 

            Gateway="172.21.250.1" NetworkMask="255.255.255.0" Location="WA1">

            <IPAddresses>

                <IPAddress Address="172.21.250.2" AddressType="RIP" 

                IsClaimed="false" ServerName="" />

                <IPAddress Address="172.21.250.3" AddressType="RIP" 

                IsClaimed="true" ServerName="DEMOFIRST01" />

            </IPAddresses>

        </NetworkDetails>

    </NetworkDetailsResponse>

## Status Codes

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