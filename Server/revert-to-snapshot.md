{{{
  "title": "RevertToSnapshot",
  "date": "2-7-2013",
  "author": "Troy Schneringer",
  "attachments": []
}}}

Reverts to a named snapshot for a specified server.

## URL

    REST: https://api.ctl.io/REST/Server/RevertToSnapshot/<format>
    SOAP: https://api.ctl.io/SOAP/Server.asmx?op=RevertToSnapshot

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
      <td>The alias of the account that owns the server. If not provided it will assume the account to which the API user is mapped. Providing this value gives you the ability to access servers in your sub accounts</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Name</td>
      <td>String</td>
      <td>The name of the Server.</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>SnapshotName</td>
      <td>String</td>
      <td>The name of the Snapshot to revert to.</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

### Examples

#### JSON

    {

      "AccountAlias": "UNK",

      "Name": "1",

      "SnapshotName": "2012-01-01-12:00:00"

    }

#### XML

    <SnapshotRequest>

        <AccountAlias>ACCT</AccountAlias>

        <Name>SERVER01</Name>

        <SnapshotName>2012-01-01-12:00:00</SnapshotName>

    </SnapshotRequest>

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
  </tbody>
</table>

### Examples

#### JSON

    {
        "Success":true,
        "Message":"Success",
        "StatusCode":0
    }

#### XML

    <APIResponse Success="true" Message="Success" StatusCode="0"/>

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
      <td>
        <p>Resource Not Found. &nbsp;</p>
        <p>A Server with the specified name cannot be found.
          <br />OR
          <br />A Snapshot with the specified name cannot be found.&nbsp;</p>
      </td>
    </tr>
    <tr>
      <td>6</td>
      <td>
        <p>Invalid Operation. &nbsp;Server must be in an active state.</p>
      </td>
    </tr>
    <tr>
      <td>100</td>
      <td>Authentication Failed. &nbsp;You must logon to the API prior to calling this method.</td>
    </tr>
    <tr>
      <td>1410</td>
      <td>Name required. &nbsp;The name parameter must be specified.</td>
    </tr>
    <tr>
      <td>1412</td>
      <td>SnapshotName required. &nbsp;The name of the snapshot must be specified.</td>
    </tr>
  </tbody>
</table>