{{{
  "title": "Get Blueprint Details",
  "date": "10-30-2014",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets the full details of the specified Blueprint.

## URL

    REST: https://api.tier3.com/REST/Blueprint/GetBlueprintDetails/<format>
    SOAP: https://api.tier3.com/SOAP/Blueprints.asmx?op=GetBlueprintDetailsResponseMsg

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
      <td>ID</td>
      <td>Int</td>
      <td>
        <p>The ID of the Blueprint to retrieve details for.</p>
      </td>
      <td>
        <p>Yes</p>
      </td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    { "ID": "1" }

#### XML

    <BlueprintRequest>

        <ID>1</ID>

    </BlueprintRequest>


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
      <td>BlueprintDetails</td>
      <td>Complex (see below)</td>
      <td>The Blueprint details (see below)</td>
    </tr>
  </tbody>
</table>

### BlueprintDetails Attributes

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
      <td>Author</td>
      <td>String</td>
      <td>The name of the company that authored the Blueprint.</td>
    </tr>
    <tr>
      <td>Capabilities</td>
      <td>String[]</td>
      <td>List of capabilities that the Blueprint has been tagged with.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>String</td>
      <td>A long description of the Blueprint.</td>
    </tr>
    <tr>
      <td>ID</td>
      <td>Int</td>
      <td>The ID of the Blueprint</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Blueprint.</td>
    </tr>
    <tr>
      <td>Status</td>
      <td>Int</td>
      <td>
        <p>The status of the Blueprint</p>
        <p>1 = Active
          <br />3 = Deleted
          <br />4 = Under Construction&nbsp;</p>
      </td>
    </tr>
    <tr>
      <td>Visibility</td>
      <td>Int</td>
      <td>
        <p>The visibility of the Blueprint</p>
        <p>1 = Public
          <br />2 = Private&nbsp;</p>
      </td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "BlueprintDetails":{

        "ID":1,

        "Name":"Blueprint 01",

        "Visibility":1,

        "Status":1

        "Author":"Tier 3",

        "Capabilities":["Web Applications","CDN"],

        "Description":"This is the first Blueprint"

      },

      "Success":true,

      "Message":"Success",

      "StatusCode":0

    }

#### XML

    <GetBlueprintDetailsResponse Success="true" Message="Success" StatusCode="0">

        <BlueprintDetails ID="1" Status="1" Visibility="1">

            <Name>Blueprint 01</Name>

            <Author>Tier 3</Author>

            <Description>This is the first Blueprint</Description>

        </BlueprintDetails>

    </GetBlueprintDetailsResponse>

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
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>5</td>
      <td>Resource Not Found. &nbsp;A Blueprint with the specified ID cannot be found.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>
