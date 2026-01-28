{{{
  "title": "GetNetworks",
  "date": "12-3-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the list of Networks mapped to the account in its Primary Data Center.

## URL

    REST: https://api.ctl.io/REST/Network/GetNetworks/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Network.asmx?op=GetNetworks

## Request

### Attributes

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | String | Short code for a particular account. If not provided, then the API user's account is used. | No |
| Location | String | The alias of the primary data center. | No |

### Examples

#### JSON (REST)

    {
        "AccountAlias": "1000",
        "Location":"WA1"
    }

#### XML (REST)

    <Networks>
        <AccountAlias>1000</AccountAlias>
        <Location>WA1</Location>
    </Networks>


#### XML (SOAP)

    <soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:xsd="http://www.w3.org/2001/XMLSchema"
        xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
      <soap12:Body>
        <Networks xmlns="http://www.tier3.com/">
            <AccountAlias>1000</AccountAlias>
            <Location>WA1</Location>
        </Networks>
      </soap12:Body>
    </soap12:Envelope>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Networks | Complex | A list of Network (see below) |

### Network Attributes

| Name | Type | Description |
| --- | --- | --- |
| Name | String | The name of the Network. This value should be used on other API methods that require a network reference. |
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

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
