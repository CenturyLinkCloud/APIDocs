{{{
  "title": "GetLocations",
  "date": "11-16-2012",
  "author": "Richard Seroter",
  "attachments": []
}}}

Gets list of all valid data center location codes that are used in subsequent Account operations. Calls to this operation must include an authorization cookie acquired from the <a href="http://help.tier3.com/entries/20339862-logon">Logon operation.</a>

## URL

    REST: https://api.tier3.com/REST/Account/GetLocations/&lt;format&gt; (format = XML | JSON)
    SOAP: https://api.tier3.com/SOAP/Account.asmx?op=LocationsResponseMsg

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
      <td>None</td>
    </tr>
  </tbody>
</table>

### Examples
<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

      xmlns:xsd="http://www.w3.org/2001/XMLSchema" 

      xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"&gt;

&lt;soap:Body&gt;

  &lt;LocationsResponseMsg xmlns="http://www.tier3.com/" /&gt;

&lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;   

</pre> 

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

<h4>JSON (REST)</h4>
<pre>{<br />     "Locations":[<br />       {"Alias":"100","Region":"Demo Region 1"},<br />       {"Alias":"101","Region":"Demo Region 2"},<br />       {"Alias":"102","Region":"Demo Region 3"}<br />     ],<br />     "Success":true,<br />     "Message":"Locations successfully queried.",<br />     "StatusCode":0<br />}</pre>
<h4>XML (REST)</h4>
<pre>&lt;LocationsResponse Success="true" Message="Locations successfully queried." StatusCode="0"&gt;<br />     &lt;Locations&gt;<br />       &lt;Location Alias="100" Region="Demo Region 1" /&gt;<br />       &lt;Location Alias="101" Region="Demo Region 2" /&gt;<br />       &lt;Location Alias="102" Region="Demo Region #3" /&gt;<br />     &lt;/Locations&gt;<br />&lt;/LocationsResponse&gt;</pre>
<h4>XML (SOAP)</h4>
<pre>&lt;soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"&gt;

&lt;soap:Body&gt;

  &lt;LocationsResponseMsgResponse xmlns="http://www.tier3.com/"&gt;

    &lt;LocationsResponseMsgResult&gt;

      &lt;Locations&gt;

        &lt;Location Alias="string" Region="string" /&gt;

        &lt;Location Alias="string" Region="string" /&gt;

      &lt;/Locations&gt;

    &lt;/LocationsResponseMsgResult&gt;

  &lt;/LocationsResponseMsgResponse&gt;

&lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;

</pre>

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
      <td>Unknown Error. &nbsp;An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>
