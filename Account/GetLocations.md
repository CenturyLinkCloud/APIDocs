{{{
  "title": "GetLocations",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets list of all valid data center location codes that are used in subsequent Account operations. Calls to this operation must include an authorization cookie acquired from the <a href="/api-docs#authentication-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Account/GetLocations/<format> (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Account.asmx?op=LocationsResponseMsg

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
      <td>None</td>
    </tr>
  </tbody>
</table>

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
      <td>Location[]</td>
      <td>Complex</td>
      <td>The list of locations (see below)</td>
    </tr>
  </tbody>
</table>

### Location Attributes

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
      <td>Alias</td>
      <td>String</td>
      <td>Short name associated with the data center. This is the value used as input to other Account operations.</td>
    </tr>
    <tr>
      <td>Region</td>
      <td>String</td>
      <td>Full name, or friendly name, of the data center.</td>
    </tr>
  </tbody>
</table>

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

              <Location Alias="102" Region="Demo Region #3" />

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
