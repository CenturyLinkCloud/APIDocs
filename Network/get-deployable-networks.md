{{{
  "title": "GetDeployableNetworks",
  "date": "9-15-2014",
  "author": "Luke Bakken",
  "attachments": []
}}}

Gets the list of Networks mapped to an account in any Data Center that are deployable.

## URL

    REST: https://api.ctl.io/REST/Network/GetDeployableNetworks/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Network.asmx?op=GetDeployableNetworks

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | The alias of the account that owns the network. If not provided it will assume the Account the API user is mapped to. Providing this value gives you the ability to get networks in your sub accounts. | No |
| Location | String | The Network's home datacenter alias.  If blank, the account home datacenter location is assumed. | No |

### Examples

#### JSON

    {
      "AccountAlias": "UNK",
      "Location": "UN1"
    }

#### XML

    <NetworkRequest>
        <AccountAlias>UNK</AccountAlias>
        <Location>UN1</Location>
    </NetworkRequest>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Networks | Complex (see below) | A list of Network (see below) |

### Network Attributes

| Name | Type | Description |
| --- | --- | --- |
| Name | String | The name of the Network. This value should be used on other api methods that require a network reference. |
| Description | String | The friendly name of the network if one has been configured. |
| Gateway | IPAddress | The default gateway for the network. |

### Examples

#### JSON

    {
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
    }

#### XML

    <GetNetworksResponse Success="true" Message="Networks successfully queried." StatusCode="0">
        <Networks>
            <Network Name="vlan_1114_10.81.14" Description="vlan_1114_10.81.14" Gateway="10.81.14.1" Location="UN1" AccountAlias="UNK"/>
            <Network Name="vlan_1241_10.81.141" Description="vlan_1241_10.81.141" Gateway="10.81.141.1" Location="UN1" AccountAlias="UNK"/>
        </Networks>
    </GetNetworksResponse>

## Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
