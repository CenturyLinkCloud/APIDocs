{{{
  "title": "GetLocations",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets list of all valid data center location codes that are used in subsequent Account operations. Calls to this operation must include an authorization cookie acquired from the [Logon operation](../Authentication/logon.md).

## URL

    REST: https://api.ctl.io/REST/Account/GetLocations/<format> (format = XML | JSON)
    SOAP: https://api.ctl.io/SOAP/Account.asmx?op=LocationsResponseMsg

## Request

### Attributes

None

### Examples

#### XML (SOAP)</h4>

    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:xsd="http://www.w3.org/2001/XMLSchema"
          xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
      <soap:Body>
        <LocationsResponseMsg xmlns="http://www.tier3.com/" />
      </soap:Body>
    </soap:Envelope>

## Response

### Attributes

| Name | Type | Description |
| --- | --- | --- |
| Success | Boolean | True if the request was successful, otherwise False. |
| Message | String | A description of the result. The contents of this field does not contain any actionable information, it is purely intended to provide a human readable description of the result. |
| StatusCode | Int | This value will help to identify any errors which were encountered while processing the request. The value of '0' indicates success, all non-zero StatusCodes indicate an error state. |
| Location[] | Complex | The list of locations (see below) |

### Location Attributes

| Name | Type | Description |
| --- | --- | --- |
| Alias | String | Short name associated with the data center. This is the value used as input to other Account operations. |
| Region | String | Full name, or friendly name, of the data center. |

### Examples

#### JSON (REST)

    {
      "Locations":[
        {
          "Alias":"100",
          "Region":"Demo Region 1"
        },
        {
          "Alias":"101",
          "Region":"Demo Region 2"
        },
        {
          "Alias":"102",
          "Region":"Demo Region 3"
        }
      ],
      "Success":true,
      "Message":"Locations successfully queried.",
      "StatusCode":0
    }

#### XML (REST)

    <LocationsResponse Success="true" Message="Locations successfully queried." StatusCode="0">
        <Locations>
            <Location Alias="100" Region="Demo Region 1" />
            <Location Alias="101" Region="Demo Region 2" />
            <Location Alias="102" Region="Demo Region 3" />
        </Locations>
    </LocationsResponse>

#### XML (SOAP)

    <soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
      <soap:Body>
        <LocationsResponseMsgResponse xmlns="http://www.tier3.com/">
          <LocationsResponseMsgResult>
            <Locations>
              <Location Alias="string" Region="string" />
              <Location Alias="string" Region="string" />
            </Locations>
          </LocationsResponseMsgResult>
        </LocationsResponseMsgResponse>
      </soap:Body>
    </soap:Envelope>

### Status Codes

| Status Code | Description |
| --- | --- |
| 0 | Request was successfully processed |
| 2 | Unknown Error.  An application error occurred processing your request, contact support to resolve the issue. |
| 100 | Authentication Failed.  You must logon to the API prior to calling this method. |
