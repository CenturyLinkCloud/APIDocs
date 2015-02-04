{{{
  "title": "GetGroups",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Gets a list of all groups with the specified search criteria.

## URL

    REST: https://api.tier3.com/REST/Group/GetGroups/<format>
    SOAP: https://api.tier3.com/SOAP/Group.asmx?op=GetGroups

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
      <td>The alias of the account that owns the groups. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access groups in your sub accounts.</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Location</td>
      <td>String</td>
      <td>The data center location to query for groups.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "AccountAlias": "UNK",

      "Location": "DC1"

    }

#### XML

    <GetGroupsRequest>

        <AccountAlias>ACCT</AccountAlias>

        <Location>WA1</Location>

    </GetGroupsRequest>

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
      <td>HardwareGroups</td>
      <td>Complex</td>
      <td>A list of Hardware Groups (see below)</td>
    </tr>
  </tbody>
</table>

### Hardware Group Attributes

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
      <td>ID</td>
      <td>Int</td>
      <td>The ID of the Group.</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Blueprint.</td>
    </tr>
    <tr>
      <td>ParentID</td>
      <td>Int</td>
      <td>The ID of the parent Group.</td>
    </tr>
    <tr>
      <td>IsSystemGroup</td>
      <td>Bool</td>
      <td>Denotes a required system Group.</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {
      
      "Groups": [

        {
          "ID":1,

          "Name":"Group 01",

          "ParentID":0,

          "IsSystemGroup":true

        },

        {
          "ID":2,

          "Name":"Group 02",

          "ParentID":1,

          "IsSystemGroup":false

        },
      ],

      "Success":true,

      "Message":"Success",

      "StatusCode":0

    }

#### XML

    <GetGroupsResponse Success="true" Message="Success" StatusCode="0">

      <HardwareGroups>

        <HardwareGroup ID="1" Name="Group 01" ParentID="0"&nbsp;IsSystemGroup="true" />

        <HardwareGroup ID="2" Name="Group 02" ParentID="1"&nbsp;IsSystemGroup="false"/>

      </HardwareGroups>

    </GetGroupsResponse>

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
      <td>Unknown Error - An application error occurred processing your request, contact Tier3 support to resolve the issue.</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Invalid Request Format. This value indicates that the XML or JSON requests do not match the expected format.</td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed - You must logon to the API prior to calling this method.</td>
    </tr>
  </tbody>
</table>