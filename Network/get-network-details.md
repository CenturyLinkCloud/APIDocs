{{{
  "title": "GetNetworkDetails",
  "date": "5-1-2013",
  "author": "Peter Kowalczyk",
  "attachments": []
}}}

Gets the details for a Network and its IP Addresses.

## URL

    REST: https://api.ctl.io/REST/Network/GetNetworkDetails/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Network.asmx?op=GetNetworkDetailsResponseMsg

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the network. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to get networks in your sub accounts. | No |
| Location | String | The Network's home datacenter alias.  If blank, the account home datacenter location is assumed. | No |
| Name | String | The Network name. | Yes |

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

| Name | Type | Description
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| NetworkDetails | Complex | The NetworkDetails (see below) |

### NetworkDetails Attributes

| Name | Type | Description |
| --- | --- | --- |
| Name | String | The Network name. |
| Description | String | The friendly name of the network if one has been configured. |
| Gateway | String | The default gateway for the network. |
| NetworkMask | String | The network mask. |
| Location | String | The Network's home datacenter alias. |
| IPAddresses | String | A list of IPAddress (see below) |

### IPAddress Attributes

| Name | Type | Description |
| --- | --- | --- |
| Address | String | The IP Address. |
| AddressType | String | The type of the IP Address<br/>RIP - Real IP (internal IP configured on the VLAN)<br/>MIP - Mapped IP (external IP configured on the Firewall)<br/>VIP - Virtual IP (external IP configured on the Load Balancer) |
| IsClaimed | Boolean | Indicates if the address is claimed or available. |
| ServerName | String | The name of the Server using this IP address, if applicable. |

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
        "IPAddresses: [
          {
            "Address":"172.21.250.2",
            "AddressType":"RIP",
            "IsClaimed":false,
            "ServerName":""
          },
          {
            "Address":"172.21.250.3",
            "AddressType":"RIP",
            "IsClaimed":true,
            "ServerName":"DEMOFIRST01"
          }
        ]
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

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 3 | Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format. |
| 5 | Resource Not Found.  A Network with the specified name cannot be found. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
| 1510 | Name Required. |
